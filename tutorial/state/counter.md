# 基础教程

## 计数器

<img src="/assets/images/tutorial/state/01.png"/>

* [仓库地址]()
* [BlocObserver](https://bloclibrary.dev/#/coreconcepts?id=blocobserver): 监控 state 的改变。
* [BlocProvider](https://bloclibrary.dev/#/flutterbloccoreconcepts?id=blocprovider): 为 widget 关联一个 bloc。
* [BlocBuilder](https://bloclibrary.dev/#/flutterbloccoreconcepts?id=blocbuilder): 被 `BlocBuilder`包裹的 widget 在状态改变时会被触发。

### 项目结构

```
├── counter
│   ├── counter.dart
│   ├── cubit
│   │   └── counter_cubit.dart
│   └── view
│       ├── counter_page.dart
│       └── counter_view.dart
├── counter_observer.dart
└── main.dart
```

### CounterObserver 

`CounterObserver` 用来监视 state 的变化。

`counter_observer.dart`: 

```dart
import 'package:flutter_bloc/flutter_bloc.dart';

/// Observe state changes with `BlocObserver`
class CounterObserver extends BlocObserver {
  @override
  void onChange(BlocBase bloc, Change change) {
    super.onChange(bloc, change);
    print('${bloc.runtimeType} $change');
  }
}
```

### main.dart

在`main.dart`中，初始化 `CounterObserver`，并替换掉`runApp()`。

```dart
import 'package:bloc_example/counter/view/counter_page.dart';
import 'package:bloc_example/counter_observer.dart';
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

void main() {
  /// 初始化 `CounterObserver`
  Bloc.observer = CounterObserver();
  runApp(CounterApp());
}

class CounterApp extends MaterialApp {
  CounterApp() : super(home: CounterPage());
}
```

### CounterPage

`CounterPage` 的职责就是 创建一个 `CounterCubit` 并把它提供给`CounterView`

`CounterPage` 在这里就相当于一个中间连接的桥梁。

`/counter/view/counter_page.dart`:

```dart
import 'package:bloc_example/counter/cubit/counter_cubit.dart';
import 'package:bloc_example/counter/view/counter_view.dart';
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

/// `CounterPage` 的职责就是 创建一个 `CounterCubit` 并把它提供给`CounterView`
/// `CounterPage` 在这里就相当于一个中间连接的桥梁。
class CounterPage extends StatelessWidget {
  const CounterPage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return BlocProvider(
      create: (_) => CounterCubit(),
      child: CounterView(),
    );
  }
}
```

### CounterCubit

在`CounterCubit` 中，处理逻辑并且通过`emit`发送信号到关联的 widget 。

`/counter/cubit/counter_cubit.dart`: 

```dart
import 'package:flutter_bloc/flutter_bloc.dart';

class CounterCubit extends Cubit<int> {
  /// `CounterCubit`的初始化状态设置为 `0`
  CounterCubit() : super(0);

  /// Add 1 to the current state.
  void increment() => emit(state + 1);

  /// Subtract 1 from the current state.
  void decrement() => emit(state - 1);
}
```

### CounterView

`CounterView` 的责任就是响应 `CounterCubit`返回的状态，并且与`CounterCubit`进行交互。

`/counter/view/counter_view.dart`:

```dart
import 'package:bloc_example/counter/cubit/counter_cubit.dart';
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

/// `CounterView` 的责任就是响应 `CounterCubit`返回的状态，并且与`CounterCubit`进行交互。
class CounterView extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final textTheme = Theme.of(context).textTheme;

    return Scaffold(
      appBar: AppBar(title: const Text('Counter')),
      body: Center(
        /// `BlocBuilder` 包裹 `Text` widget是为了更新 `text`的状态。
        /// `BlocBuilder` 只用在这里是因为当`CounterCubit`改变状态时，只有这里的 `Text`才需要从建状态。
        child: BlocBuilder<CounterCubit, int>(
          builder: (context, state) {
            return Text('$state', style: textTheme.headline2);
          },
        ),
      ),
      floatingActionButton: Column(
        mainAxisAlignment: MainAxisAlignment.end,
        crossAxisAlignment: CrossAxisAlignment.end,
        children: <Widget>[
          FloatingActionButton(
            key: const Key('counterView_increment_floatingActionButton'),
            child: const Icon(Icons.add),
            onPressed: () => context.read<CounterCubit>().increment(),
          ),
          const SizedBox(height: 8),
          FloatingActionButton(
            key: const Key('counterView_decrement_floatingActionButton'),
            child: const Icon(Icons.remove),
            onPressed: () => context.read<CounterCubit>().decrement(),
          ),
        ],
      ),
    );
  }
}
```

### counter.dart

`counter.dart`的作用就是导出所有 public 的dart文件。

```dart
/// `counter.dart`的作用就是导出所有 public 的dart文件。
export 'cubit/counter_cubit.dart';
export 'view/counter_page.dart';
```

