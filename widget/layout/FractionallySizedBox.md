
* [FractionallySizedBox Class](https://api.flutter.dev/flutter/widgets/FractionallySizedBox-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/PEsY654EGZ0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
const FractionallySizedBox({
  Key key,
  AlignmentGeometry alignment: Alignment.center, // 对齐方式
  double widthFactor, // 宽度因子
  double heightFactor, // 高度因子
  Widget child
})
```

Widget 会根据现有空间来调整 child 的尺寸，所以就算为 child 设置了尺寸数值，也不起作用。

* 设置了具体的宽高因子，`具体的宽高=现有的空间宽高X因子`。
* 没有设置宽高因子，则填满可用区域。

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
        appBar: new AppBar(
          title: Text('data'),
        ),
        body: new Container(
          color: Colors.red,
          height: 200.0,
          width: 200.0,
          child: new FractionallySizedBox(
            alignment: Alignment.topCenter,
            widthFactor: 0.5, //宽度因子
            heightFactor: 1.5, //高度因子
            child: new Container(
              color: Colors.blue,
            ),
          ),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/51.png" width = "50%" height = "50%"/>
