
# Padding(填充布局)
Padding(填充布局)： 用于处理容器与其子元素之间的间距，与`padding`对应的属性是 `margin` 属性，`margin`是处理容器与其他组件之间的间距。

* [Padding (Flutter Widget of the Week)](https://www.youtube.com/watch?v=oD5RtLhhubg)
* [Padding Class](https://api.flutter.dev/flutter/widgets/Padding-class.html)
* [Padding Demo](https://dartpad.dartlang.org/8f4870b99659769303f31d3036fea79a)

<img src="/assets/images/flutter/72.png" width = "25%" height = "25%"/>

| 属性|类型|说明|
| --- | --- | --- |
|padding|EdgeInsetsGeometry|填充的值可以用`EdgeInsets`方法，例如：`EdgeInsets.all(6.0)`将容器的上下左右填充设置为6.0|

```dart
// 所有方向
const EdgeInsets.all(double value)
// 分别定义各个方向的边框
const EdgeInsets.only({double left: 0.0,double top: 0.0,double right: 0.0,double bottom: 0.0})
// 自定义垂直、水平方向
const EdgeInsets.symmetric({double vertical: 0.0,double horizontal: 0.0})
// 根据机型屏幕尺寸定义
EdgeInsets.fromWindowPadding(ui.WindowPadding padding, double devicePixelRatio)
```

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

<img src="/assets/images/flutter/30.png" /> <!-- width = "25%" height = "25%" -->
