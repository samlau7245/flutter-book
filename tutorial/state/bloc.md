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

### Bloc-data架构说明

[参考文档](https://bloclibrary.dev/#/./architecture)

<img src="/assets/images/tutorial/state/02.png"/>

使用`bloc`库,可以让项目分为三层：

* UI: 展示层
* Bloc: 业务逻辑层
* Data: 数据层
  * Repository 
  * Data Provider

#### Data: 数据层

数据层的责任就是从一个或者多个源中获取/操作数据。 数据层算是整个项目中的最低层，负责和数据库进行交互、请求网络和其他一些数据源的交互。

##### Data Provider

`Data Provider` 一般负责提供一些简单的`CURD`操作的API。

```dart
class SimpleDataProvider {
  Future<RawData> createData() async {
    // DB操作或者网络操作。
    return RawData();
  }

  Future<RawData> readData() async {
    // DB操作或者网络操作。
    return RawData();
  }

  Future<RawData> updateData() async {
    // DB操作或者网络操作。
    return RawData();
  }

  Future<RawData> deleteData() async {
    // DB操作或者网络操作。
    return RawData();
  }
}
```

##### Repository

`Repository` 会提供一个`wrapper`包装一个或者多个`Data Provider`。

```dart
class Repository {
    final DataProviderA dataProviderA;
    final DataProviderB dataProviderB;

    Future<Data> getAllDataThatMeetsRequirements() async {
        final RawDataA dataSetA = await dataProviderA.readData();
        final RawDataB dataSetB = await dataProviderB.readData();

        final Data filteredData = _filterData(dataSetA, dataSetB);
        return filteredData;
    }
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

### 构造函数

```dart
class BlocProvider<T extends BlocBase<Object?>> extends SingleChildStatelessWidget with BlocProviderSingleChildWidget {
  BlocProvider({
    Key? key,
    required Create<T> create,
    this.child,
    this.lazy,
  });
}
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

## BlocListener

`BlocListener` 调用`listener`来监听状态`State`的改变。一般使用的场景： `navigation`、展示`SnackBar`、 展示`Dialog`...

每次状态改变时`listener`都会被调用。(**除了初始化状态**)

```dart
BlocListener<BlocA, BlocAState>(
  listenWhen: (previous, current) {
    // return true/false to determine whether or not
    // to invoke listener with state
  },
  listener: (context, state) {
    // do stuff here based on BlocA's state
  }
  child: Container(),
)
```

代码示例：

```dart
class LoginForm extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocListener<LoginBloc, LoginState>(
      listener: (context, state) {
        if (state.status.isSubmissionFailure) {
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(
              SnackBar(content: Text('Authentication Failure')),
            );
        }
      },
      child: Align(
        alignment: Alignment(0, -1 / 3),
        child: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            _UsernameInput(),
            const Padding(padding: EdgeInsets.all(12)),
            _PasswordInput(),
            const Padding(padding: EdgeInsets.all(12)),
            _LoginButton(),
          ],
        ),
      ),
    );
  }
}
```

### 继承关系

StatefulWidget -> SingleChildStatefulWidget -> BlocListenerBase -> BlocListener

### 构造函数

```dart
/// Signature for the `listener` function which takes the `BuildContext` along
/// with the `state` and is responsible for executing in response to
typedef BlocWidgetListener<S> = void Function(BuildContext context, S state);

typedef BlocListenerCondition<S> = bool Function(S previous, S current);

class BlocListener<B extends BlocBase<S>, S> extends BlocListenerBase<B, S> with BlocListenerSingleChildWidget {
  const BlocListener({
    Key? key,
    required BlocWidgetListener<S> listener,
    B? bloc,
    BlocListenerCondition<S>? listenWhen,
    Widget? child,
  });
}
```

## MultiBlocListener
## RepositoryProvider

`RepositoryProvider` Widget 提供了一个仓库或者存储的位置，让它的`children`可以通过`RepositoryProvider.of<T>(context)`来获取


```dart
RepositoryProvider(
  create: (context) => RepositoryA(),
  child: ChildA(),
);
```

示例代码：

```dart
@override
Widget build(BuildContext context) {
  /// `RepositoryProvider` 的功能是： 提供一个`AuthenticationRepository`单例，给后续的逻辑使用。
  return RepositoryProvider.value(
    value: authenticationRepository,
    child: BlocProvider(
      create: (_) => AuthenticationBloc(
        authenticationRepository: authenticationRepository,
        userRepository: userRepository,
      ),
      child: AppView(),
    ),
  );
}
```

### 继承关系

Widget -> StatelessWidget -> SingleChildStatelessWidget -> InheritedProvider -> Provider -> RepositoryProvider

### 构造函数

```dart
/// A function that creates an object of type [T].
typedef Create<T> = T Function(BuildContext context);

class RepositoryProvider<T> extends Provider<T> with RepositoryProviderSingleChildWidget {
  
  RepositoryProvider({
    Key? key,
    required Create<T> create,
    Widget? child,
    bool? lazy,
  }));
  
  RepositoryProvider.value({
    Key? key,
    required T value,
    Widget? child,
  });
}
```

## MultiRepositoryProvider














































































