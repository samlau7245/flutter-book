
# [FloatingActionButton(悬停按钮组件)](https://api.flutter.dev/flutter/material/FloatingActionButton-class.html)

| 属性|类型|默认值|说明|
| --- | --- | --- | --- |
|child|Widget|||
|tooltip||||
|foregroundColor||||
|backgroundColor||||
|elevation||||
|hignlightElevation||||
|onPressed||||
|shape||||

这个组件构造方法：

```dart
FloatingActionButton();
FloatingActionButton.extended();
```

[示例代码](https://codepen.io/samlau7245/pen/oNjPbwB)

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
    return Scaffold(
      appBar: AppBar(
        title: Text("FloatingActionButton Demo"),
      ),
      /*floatingActionButton: FloatingActionButton(
        onPressed: () {},
        child: Icon(Icons.navigation),
        backgroundColor: Colors.green,
      ),*/
      floatingActionButton: FloatingActionButton.extended(
        onPressed: () {},
        label: Text('Approve'),
        icon: Icon(Icons.thumb_up),
        backgroundColor: Colors.pink,
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
        floatingActionButton: new Builder(builder: (BuildContext context){
          return new FloatingActionButton(
            child: const Icon(Icons.add),
            tooltip: 'Click Tip',
            foregroundColor: Colors.red,
            backgroundColor: Colors.blue,
            elevation: 7.0,// 未点击阴影值
            highlightElevation: 14.0,// 点击阴影值
            mini: false,
            shape: new CircleBorder(),
            isExtended: false,
            onPressed: (){
              Scaffold.of(context).showSnackBar(
                new SnackBar(content: new Text('data'))
              );
            },
          );
        }),
        floatingActionButtonLocation: FloatingActionButtonLocation.centerFloat,// 居中
      ),
    );
  }
}
```

把`FloatingActionButton`写在`Builder`组件里面为了使`SnackBar`有效果，因为这个类是`StatelessWidget`。也可以通过下面的代码实现，使用`StatefulWidget`：

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

// MyApp 不做状态处理，所以继承 StatelessWidget
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Demo',
      home: new LoginPage(title: 'This is title!',),
    );
  }
}
// 主体需要做状态处理，继承 StatefulWidget
class LoginPage extends StatefulWidget {
  LoginPage({Key key,this.title}) : super(key:key);
  final String title;

  @override
  _LoginPageState createState() => new _LoginPageState();
}
class _LoginPageState extends State<LoginPage> {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: Text(widget.title),
      ),
      body: new Center(
        child: FlatButton(onPressed: (){
          _neverSatisfied(context);
        }, child: new Text('FlatButton'))
      ),
    );
  }
}


Future _neverSatisfied(BuildContext context) async {
  return showDialog(
      context: context,
      barrierDismissible: false,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Rewind and remember'),
          content: SingleChildScrollView(
            child: ListBody(
              children: <Widget>[
                Text('You will never be satisfied.'),
                Text('You\’re like me. I’m never satisfied.'),
              ],
            ),
          ),
          actions: <Widget>[
            FlatButton(
              child: Text('Regret'),
              onPressed: () {
                Navigator.of(context).pop();
              },
            ),
          ],
        );
      });
}
```

<img src="/assets/images/flutter/20.gif"/>
