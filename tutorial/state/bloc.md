# package: bloc

## Cubit

`Cubit` 的责任就是把输入的 `Event` 流转化为`State`流；详细的流程图：

<img src="/assets/images/tutorial/state/03.png"/>

### 继承关系

BlocBase -> Cubit

```dart
abstract class Cubit<State> extends BlocBase<State> {}
```

### BlocObserver

`BlocObserver` 可以让我们在一个地方观察、修改 `Bloc`中所有的 `Change`。

```dart
class SimpleBlocObserver extends BlocObserver {
  @override
  void onTransition(Bloc bloc, Transition transition) {
    super.onTransition(bloc, transition);
  }

  @override
  void onError(BlocBase bloc, Object error, StackTrace stackTrace) {
    super.onError(bloc, error, stackTrace);
  }
}
```

## Bloc

`Bloc` 的责任就是把输入的 `Event` 流转化为`State`流；详细的流程图：

<img src="/assets/images/tutorial/state/02.png"/>

### 继承关系

BlocBase -> Bloc

```dart
abstract class Bloc<Event, State> extends BlocBase<State> {}
```

### transform 方法

实现 `transform` 方法，可以让我们在调用`mapEventToState`方法之前对`Stream`进行转换。

```dart
@override
Stream<Transition<TimerEvent, TimerState>> transformEvents(
    Stream<TimerEvent> events, transitionFn) {
  return super.transformEvents(events.distinct(), transitionFn);
}
```

## Cubit、Bloc对比

> 什么时候用`Cubit`， 什么时候使用`Bloc`？

### Cubit

对于 `CounterCubit`用`Bloc`的方式实现：

```dart
enum CounterEvent { increment, decrement }
class CounterBloc extends Bloc<CounterEvent, int> {
  CounterBloc() : super(0);
  @override
  Stream<int> mapEventToState(CounterEvent event) async* {
    switch (event) {
      case CounterEvent.increment:
        yield state + 1;
        break;
      case CounterEvent.decrement:
        yield state - 1;
        break;
      default:
    }
  }
}
```

对比与`CounterCubit`: 

```dart
class CounterCubit extends Cubit<int> {
  CounterCubit() : super(0);
  void increment() => emit(state + 1);
  void decrement() => emit(state - 1);
}
```

**在功能非常简单的时候使用`Cubit`，更容易让人理解，代码编写也更少。**

在一些列状态都需要改变时，可以使用`Bloc`。

# package: flutter_bloc 

## BlocBuilder

`BlocBuilder`是一个需要需要传入`BlocBase`和`builder`的`StatefulWidget`，通过响应的`State`状态来构建 Widget 树。

使用`BlocBuilder`：

```dart
BlocBuilder<BlocA, BlocAState>(
  buildWhen: (previous, current) {
    // return true/false to determine whether or not
    // to rebuild the widget with state
  },
  builder: (context, state) {
    // return widget here based on BlocA's state
  }
)
```

### 继承关系

StatefulWidget -> BlocBuilderBase -> BlocBuilder

代码结构：

```dart
class BlocBuilder<B extends BlocBase<S>, S> extends BlocBuilderBase<B, S> {}
```

## BlocProvider

> **BlocProvider**负责把 `Bloc`或`Cubit`和`Widget`关联在一起。

```dart
BlocProvider(
  create: (BuildContext context) => BlocA(),
  child: ChildA(),
);
```

从定义中来看`required Create<T> create,`中的`T`是继承于`BlocBase`类实现的:

```dart
class BlocProvider<T extends BlocBase<Object?>>
```
也就是说`create`函数是负责创建`Bloc`或者`Cubit`类的。

`final Widget? child;` 中 `child`Widget是用来使用`Bloc`或者`Cubit`的。

### 继承关系

StatelessWidget -> BlocProviderSingleChildWidget -> BlocProvider

```dart
class BlocProvider<T extends BlocBase<Object?>> extends SingleChildStatelessWidget with BlocProviderSingleChildWidget{}
```

## MultiBlocProvider

`MultiBlocProvider`负责把多个`BlocProvider`合并成一个。

```dart
MultiBlocProvider(
  providers: [
    BlocProvider<BlocA>(
      create: (BuildContext context) => BlocA(),
    ),
    BlocProvider<BlocB>(
      create: (BuildContext context) => BlocB(),
    ),
    BlocProvider<BlocC>(
      create: (BuildContext context) => BlocC(),
    ),
  ],
  child: ChildA(),
)
```

































































