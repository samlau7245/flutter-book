
* [Padding Class](https://api.flutter.dev/flutter/widgets/Padding-class.html)

# 构造函数

```dart
const Padding({
  Key key,
  @required EdgeInsetsGeometry padding,
  Widget child
})
```

<img src="/assets/images/flutter/72.png" width = "25%" height = "25%"/>

# 示例

[addingExample.dart](https://gitee.com/SamLearning/FlutterExample/blob/master/widgets/lib/Layout/PaddingExample.dart)

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Demo',
      home: PaddingDemo(),
    );
  }
}

class PaddingDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: Text('Padding Demo'),
      ),
      body: new Center(
        child: new Container(
          width: 300.0,
          height: 300.0,
          // 容器的上下左右填充设置为60.0
          padding: new EdgeInsets.all(30.0),
          decoration: new BoxDecoration(
            color: Colors.red,
            border: new Border.all(
              color: Colors.green,
              width: 8.0,
            ),
          ),
          child: new Container(
            color: Colors.white,
          ),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/30.png" /> 

# Padding、Margin

```dart
Widget buildTile() {
  return Container(
    color: Colors.red,
    child: Row(
      mainAxisAlignment: MainAxisAlignment.spaceBetween, //子组件的排列方式为主轴两端对齐
      children: <Widget>[
        new InkWell(
          child: new Padding(
              padding: const EdgeInsets.all(12.0),
              child: Image.asset(
                Constant.ASSETS_IMG + 'icon_close.png',
                width: 20.0,
                height: 20.0,
              )),
          onTap: () {
            // Navigator.pop(context);
          },
        ),
        new InkWell(
          child: new Padding(
              padding: const EdgeInsets.all(12.0),
              child: new Text(
                "帮助",
                style:
                    new TextStyle(fontSize: 16.0, color: Color(0xff6B91BB)),
              )),
          onTap: () {},
        ),
      ],
    ),
  );
}

Container buildInputPass() {
  return Container(
    color: Colors.orange,
    margin: const EdgeInsets.only(
      left: 20.0,
      top: 30.0,
      bottom: 20,
      right: 20.0,
    ),
    child: Text(
      "请输入账号密码请输入账号密码请输入账号密码请输入账号",
      style: TextStyle(fontSize: 24.0, color: Colors.black),
    ),
  );
}

ListView(
  children: [
    buildTile(),
    buildInputPass(),
  ],
),
```

<img src="/assets/images/widgets/41.png" /> 

从红色块和橙色块两个Widget的布局可以知道内边距和外边距的区别。

# 资料

* [Padding (Flutter Widget of the Week)](https://www.youtube.com/watch?v=oD5RtLhhubg)
* [Padding Demo](https://dartpad.dartlang.org/8f4870b99659769303f31d3036fea79a)
