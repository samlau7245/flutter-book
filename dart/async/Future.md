
[Future Class](https://api.flutter-io.cn/flutter/dart-async/Future-class.html)

`Flutter`通过`Future`实现了异步操作的功能。

# 构造函数

```dart
factory Future(FutureOr<T> computation())
factory Future.delayed(Duration duration, [FutureOr<T> computation()])
factory Future.error(Object error, [StackTrace stackTrace])
factory Future.microtask(FutureOr<T> computation())
factory Future.sync(FutureOr<T> computation())
factory Future.value([FutureOr<T> value])
```

# 方法

```dart
Stream<void> asStream() 
Future<void> catchError(Function onError, {bool test(dynamic error)}) 
dynamic noSuchMethod(Invocation invocation) 
Future<R> then<R>(FutureOr<R> onValue(void value), {Function onError}) 
Future<void> timeout(Duration timeLimit, {dynamic onTimeout()}) 
String toString() 
Future<void> whenComplete(dynamic action()) 
void whenCompleteOrCancel(VoidCallback callback) 
```

# 使用

用`Future`实现一个基本的示例：

```dart
class _FutureExampleState extends State<FutureExample> {
  Future<String> getFuture() {
    return Future.value('Future Value');
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          getFuture().then((value) {
            print(value); // flutter: Future Value
          });
        },
      ),
    );
  }
}
```

## Future.delayed 延迟

```dart
Future<String> getFuture() {
  return Future.delayed(Duration(seconds: 2), () {
    return Future.value('Future Delay!');
  });
}

getFuture().then((value) {
  print(value); // flutter: Future Delay!
});  
```

## Future.error

```dart
Future<String> getFuture() {
  Exception exception = Exception();
  return Future.error(exception);
}
```

## Future.timeout

`timeout` 设置`Future`异步处理的超时时间。

```dart
Future<String> getFuture() {
  return Future.delayed(Duration(seconds: 3), () {
    return Future.value('Future Delay!');
  });
}

getFuture().timeout(Duration(seconds: 2)).then((value) {
  print(value);
}).catchError((error) {
  print(error);
});
```

这里调用`getFuture()`方法时，设置超时时间为`2s`，所以执行方法会超时。在`catchError`中打印超时日志信息:

```dart
flutter: TimeoutException after 0:00:02.000000: Future not completed
```




























