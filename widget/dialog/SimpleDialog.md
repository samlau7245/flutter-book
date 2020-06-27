
# [SimpleDialog(简单对话框组件)](https://api.flutter.dev/flutter/material/SimpleDialog-class.html)

| 属性|类型|说明|
| --- | --- | --- |
|children|`List<Widget>`||
|title|||
|contentPadding|||
|titlePadding|||

[示例代码](https://codepen.io/samlau7245/pen/OJyoMBo)

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "FloatingActionButton Demo",
      home: HomePage(),
    );
  }
}

//////////////////////////////首页//////////////////////////////////

class HomePage extends StatefulWidget {
  HomePage({Key key}) : super(key: key);
  @override
  _HomePage createState() => new _HomePage();
}

class _HomePage extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    
    Future<void> _showDialog() async {
      await showDialog(
          context: context,
          builder: (_) {
            return SimpleDialog(
              title: Text('This is a SimpleDialog!'),
              children: <Widget>[
                SimpleDialogOption(child: Text("data")),
                SimpleDialogOption(child: Text("data")),
              ],
            );
          });
    }

    return Scaffold(
      appBar: AppBar(
        title: Text("FloatingActionButton Demo"),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          _showDialog();
        },
      ),
    );
  }
}
```

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(
          title: Text('Demo'),
        ),
        body: new Center(
          child: showDialog(),
        ),
      ),
    );
  }
}
StatelessWidget showDialog() {
  return SimpleDialog(
    title: const Text('SimpleDialog Title'),
    children: <Widget>[
      SimpleDialogOption(
        child: new Text('Line 3'),
        onPressed: () {},
      ),
      SimpleDialogOption(
        child: new Text('Line 3'),
        onPressed: () {},
      ),
      SimpleDialogOption(
        child: new Text('Line 3'),
        onPressed: () {},
      ),
    ],
  );
}
```

<img src="/assets/images/flutter/23.png" width = "25%" height = "25%"/>

> 一般对话框要封装在方法里，通过点击事件弹出。如果这一过程是异步要加上`async/await`处理。
