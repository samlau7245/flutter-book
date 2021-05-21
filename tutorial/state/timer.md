# 效果

# 结构

```
├── bloc
│   ├── timer_bloc.dart
│   ├── timer_event.dart
│   └── timer_state.dart
├── main.dart
└── ticker.dart 提供数据源
```

# pubspec.yaml

```yaml
name: bloc_timer
description: A new Flutter project.
publish_to: 'none' # Remove this line if you wish to publish to pub.dev
version: 1.0.0+1

environment:
  sdk: '>=2.12.0 <3.0.0'

dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
  flutter_bloc: ^7.0.0
  equatable: ^1.0.0
  wave: ^0.0.8

dev_dependencies:
  flutter_test:
    sdk: flutter

flutter:
  uses-material-design: true
```

执行`flutter packages get`安装依赖。

* `Equatable`: 是为了防止不必要重建 widget tree的情况，[如何使用](https://bloclibrary.dev/#/faqs?id=when-to-use-equatable)。
* [wave](https://pub.dev/packages/wave): 是一个可以展示波纹的工具包。

<img src="/assets/images/tutorial/state/04.gif"/>

# ticker.dart 数据源

`ticker.dart` 是本 demo 的数据来源，它会返回一组`Stream`数据流。

```dart
/// 提供数据源
/// `Ticker`: 钟表, `tick tack` (钟表)滴答声
class Ticker {
  /// `tick`: 记号、滴答声
  Stream<int> tick({int? ticks}) {
    /// `periodic`: 周期的、定期的
    /// `Stream`: (数据)流
    return Stream.periodic(Duration(seconds: 1), (x) => ticks! - x - 1)
        .take(ticks!);
  }
}
```

`tick` 函数会周期性(每秒)的返回一个`Stream`。

# timer_event.dart 定时器的事件

* `TimerStarted`:  通知 TimerBloc 计时器应该开始
* `TimerPaused`: 通知 TimerBloc 计时器应该暂停
* `TimerResumed`: 通知 TimerBloc 计时器应该重启
* `TimerReset`: 通知 TimerBloc 计时器应该重置
* `TimerTicked`: 通知 TimerBloc 计时器已经开始计时，需要实时更新状态。

```dart
part of 'timer_bloc.dart';

abstract class TimerEvent extends Equatable {
  const TimerEvent();

  @override
  List<Object> get props => [];
}

// TimerStarted — informs the TimerBloc that the timer should be started.

class TimerStarted extends TimerEvent {
  final int duration;

  TimerStarted({required this.duration});

  @override
  String toString() => 'TimerStarted {duration : $duration}';
}

// TimerPaused — informs the TimerBloc that the timer should be paused.
class TimerPaused extends TimerEvent {}

// TimerResumed — informs the TimerBloc that the timer should be resumed.
class TimerResumed extends TimerEvent {}

// TimerReset — informs the TimerBloc that the timer should be reset to the original state.
class TimerReset extends TimerEvent {}

// TimerTicked — informs the TimerBloc that a tick has occurred and that it needs to update its state accordingly.
class TimerTicked extends TimerEvent {
  final int duration;
  const TimerTicked({required this.duration});

  @override
  List<Object> get props => [duration];

  @override
  String toString() => 'TimerTicked { duration: $duration }';
}
```

# timer_state.dart 定义 Bloc 的状态

* `TimerInitial`:  准备开始计时。 用户可以`开始`计时。
* `TimerRunInProgress`: 正在计时中。用户可以`暂停`、`重置`计时器，也可以看到剩余的秒数。
* `TimerRunPause`: 暂停。 用户可以`重新开始`、`重置`计时器。
* `TimerRunComplete`: 完成。 用户可以`开始`计时。

```dart
part of 'timer_bloc.dart';

abstract class TimerState extends Equatable {
  final int duration;

  const TimerState({required this.duration});

  @override
  List<Object> get props => [];
}

// TimerInitial — ready to start counting down from the specified duration.
class TimerInitial extends TimerState {
  const TimerInitial(int duration) : super(duration: duration);

  @override
  String toString() => 'TimerInitial { duration: $duration}';
}

// TimerRunInProgress — actively counting down from the specified duration.
class TimerRunInProgress extends TimerState {
  const TimerRunInProgress(int duration) : super(duration: duration);

  @override
  String toString() => 'TimerRunInProgress { duration: $duration}';
}

// TimerRunPause — paused at some remaining duration.
class TimerRunPause extends TimerState {
  const TimerRunPause(int duration) : super(duration: duration);

  @override
  String toString() => 'TimerRunPause { duration: $duration}';
}

// TimerRunComplete — completed with a remaining duration of 0.
class TimerRunComplete extends TimerState {
  const TimerRunComplete() : super(duration: 0);
}
```

# timer_bloc.dart

## 设置 Bloc 初始化状态

```dart
class TimerBloc extends Bloc<TimerEvent, TimerState> {
  /// 1. 定义 `TimerBloc` 的初始化状态`TimerInitial`； 这个demo中，我们把计时器区间设置在[0,60]秒。
  static const int _duration = 60;
  TimerBloc() : super(TimerInitial(_duration));
  @override
  Stream<TimerState> mapEventToState(TimerEvent event) async* {}
}
```

## 把数据源依赖到Bloc

```dart
import 'dart:async';

import 'package:bloc/bloc.dart';
import 'package:bloc_timer/ticker.dart';
import 'package:equatable/equatable.dart';
import 'package:flutter/material.dart';

part 'timer_event.dart';
part 'timer_state.dart';

class TimerBloc extends Bloc<TimerEvent, TimerState> {
  /// 1. 定义 `TimerBloc` 的初始化状态`TimerInitial`； 这个demo中，我们把计时器区间设置在[0,60]秒。
  static const int _duration = 60;

  /// 2. 把 `Ticker` 依赖到构造函数中。
  final Ticker _ticker;

  TimerBloc({required ticker})
      : assert(ticker != null),
        _ticker = ticker,
        super(TimerInitial(_duration));

  @override
  Stream<TimerState> mapEventToState(TimerEvent event) async* {}
}
```

## 给 Ticker 创建一个 StreamSubscription、实现Event->State

```dart
import 'dart:async';
import 'package:bloc/bloc.dart';
import 'package:equatable/equatable.dart';
import 'package:flutter_timer/ticker.dart';

part 'timer_event.dart';
part 'timer_state.dart';

class TimerBloc extends Bloc<TimerEvent, TimerState> {
  final Ticker _ticker;
  static const int _duration = 60;

  StreamSubscription<int>? _tickerSubscription;

  TimerBloc({required Ticker ticker})
      : _ticker = ticker,
        super(TimerInitial(_duration));

  @override
  void onTransition(Transition<TimerEvent, TimerState> transition) {
    print(transition);
    super.onTransition(transition);
  }

  @override
  Stream<TimerState> mapEventToState(
    TimerEvent event,
  ) async* {
    if (event is TimerStarted) {
      yield* _mapTimerStartedToState(event);
    } else if (event is TimerPaused) {
      yield* _mapTimerPausedToState(event);
    } else if (event is TimerResumed) {
      yield* _mapTimerResumedToState(event);
    } else if (event is TimerReset) {
      yield* _mapTimerResetToState(event);
    } else if (event is TimerTicked) {
      yield* _mapTimerTickedToState(event);
    }
  }

  @override
  Stream<Transition<TimerEvent, TimerState>> transformEvents(
      Stream<TimerEvent> events, transitionFn) {
    return super.transformEvents(events.distinct(), transitionFn);
  }

  @override
  Future<void> close() {
    _tickerSubscription?.cancel();
    return super.close();
  }

  Stream<TimerState> _mapTimerStartedToState(TimerStarted start) async* {
    yield TimerRunInProgress(start.duration);
    _tickerSubscription?.cancel();
    _tickerSubscription = _ticker
        .tick(ticks: start.duration)
        .listen((duration) => add(TimerTicked(duration: duration)));
  }

  Stream<TimerState> _mapTimerPausedToState(TimerPaused pause) async* {
    if (state is TimerRunInProgress) {
      _tickerSubscription?.pause();
      yield TimerRunPause(state.duration);
    }
  }

  Stream<TimerState> _mapTimerResumedToState(TimerResumed resume) async* {
    if (state is TimerRunPause) {
      _tickerSubscription?.resume();
      yield TimerRunInProgress(state.duration);
    }
  }

  Stream<TimerState> _mapTimerResetToState(TimerReset reset) async* {
    _tickerSubscription?.cancel();
    yield TimerInitial(_duration);
  }

  Stream<TimerState> _mapTimerTickedToState(TimerTicked tick) async* {
    yield tick.duration > 0
        ? TimerRunInProgress(tick.duration)
        : TimerRunComplete();
  }
}
```

# main.dart

```dart
import 'package:bloc_timer/bloc/timer_bloc.dart';
import 'package:bloc_timer/ticker.dart';
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Timer',
      home: BlocProvider(
        create: (_) => TimerBloc(ticker: Ticker()),
        child: Timer(),
      ),
    );
  }
}
```

`BlocProvider` 负责把 `Bloc`和 `Widget` 连接在一起。

## Timer 

```dart
class Timer extends StatefulWidget {
  @override
  _TimerState createState() => _TimerState();
}

class _TimerState extends State<Timer> {
  static const TextStyle timerTextStyle = TextStyle(
    fontSize: 60,
    fontWeight: FontWeight.bold,
  );

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Timer')),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        crossAxisAlignment: CrossAxisAlignment.center,
        children: [
          Padding(
            padding: EdgeInsets.symmetric(vertical: 100.0),
            child: Center(
              child:
                  BlocBuilder<TimerBloc, TimerState>(builder: (context, state) {
                final String minStr = ((state.duration / 60) % 60)
                    .floor()
                    .toString()
                    .padLeft(2, '0');

                final String secStr =
                    (state.duration % 60).floor().toString().padLeft(2, '0');

                return Text(
                  '$minStr:$secStr',
                  style: timerTextStyle,
                );
              }),
            ),
          ),
        ],
      ),
    );
  }
}
```

<img src="/assets/images/tutorial/state/05.png"/>

