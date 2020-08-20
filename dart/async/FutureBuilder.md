
[FutureBuilder Class](https://api.flutter-io.cn/flutter/widgets/FutureBuilder-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/ek8ZPdWj4Qo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

`FutureBuilder`是一个将异步操作和异步UI更新结合在一起的类，通过它我们可以将网络请求，数据库读取等的结果更新的页面上。

# 构造函数

```dart
const FutureBuilder<T>({
	Key key,
	Future<T> future,
	T initialData,
	@required AsyncWidgetBuilder<T> builder
})

Widget AsyncWidgetBuilder (
	BuildContext context,
	AsyncSnapshot<T> snapshot
)
```

## AsyncSnapshot

`AsyncSnapshot`中包含了异步处理的信息。

### 构造函数

```dart
const AsyncSnapshot.nothing()
const AsyncSnapshot.withData(ConnectionState state, T data)
const AsyncSnapshot.withError(ConnectionState state, Object error)
```

### 属性、方法

```dart
ConnectionState connectionState; // 当前异步处理的连接状态
T data; // 最新接收到的数据
Object error; // 最新接收到的Error
bool hasData; // 判断是否有数据
bool hasError; // 判断是否报错
int hashCode; // HashCode
T requireData; // 最新接收的数据

enum ConnectionState {
  none,
  waiting,
  active,
  done,
}

AsyncSnapshot<T> inState(ConnectionState state);
```

# 示例

```dart
class FutureBuilderExample extends StatefulWidget {
  @override
  _FutureBuilderExampleState createState() => _FutureBuilderExampleState();
}

class _FutureBuilderExampleState extends State<FutureBuilderExample> {
  Future<String> getFuture() {
    return Future.delayed(Duration(seconds: 2), () {
      return Future.value('Response');
    });
  }

  @override
  Widget build(BuildContext context) {
    return FutureBuilder<String>(
      builder: (_, AsyncSnapshot<String> snapshot) {
        Widget widget;
        if (snapshot.connectionState == ConnectionState.done) {
          widget = Center(
            child: Text("FutureBuilder Connect Done!+ ${snapshot.data}"),
          );
        } else {
          widget = Center(child: CircularProgressIndicator());
        }

        return Scaffold(
          appBar: AppBar(
            title: Text("FutureBuilderExample"),
          ),
          body: widget,
        );
      },
      future: getFuture(),
    );
  }
}
```

<img src="/assets/images/dart/01.gif"/>




























