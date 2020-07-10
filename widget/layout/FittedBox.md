
* [FittedBox Class](https://api.flutter.dev/flutter/widgets/FittedBox-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/T4Uehk3_wlY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
const FittedBox({
  Key key,
  BoxFit fit: BoxFit.contain, // 缩放方式
  AlignmentGeometry alignment: Alignment.center, // 设置对齐方式
  Widget child
})
```

布局行为分为两种情况:

* 如果外部有约束的话，按照外部约束调整自身尺寸，然后缩放调整child，按照指定的条件进行布局。
* 如果没有外部约束条件，则跟着child尺寸一致，指定的缩放以及位置属性将不起作用。

# 示例

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(title: Text('data'),),
        body: new Container(
          color: Colors.red,
          width: 200.0,
          height: 200.0,
          child: new FittedBox(
            fit: BoxFit.scaleDown,
            alignment: Alignment.topLeft,
            child: new Container(
              color: Colors.green,
              child: new Text('Test'),
            ),
          ),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/35.png" width = "25%" height = "25%"/>