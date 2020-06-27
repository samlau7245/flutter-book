
# FractionallySizedBox(百分比布局)

`FractionallySizedBox` 组件会根据现有空间来调整child的尺寸，所以就算为child设置了尺寸数值，也不起作用。

* 设置了具体的宽高因子，`具体的宽高=现有的空间宽高X因子`。
* 没有设置宽高因子，则填满可用区域。

|属性|类型|描述|
| --- | --- | --- |
|alignment|AlignmentGeometry|对齐方式，不能为null|
|widthFactor|double|宽度因子|
|heightFactor|double|高度因子|

* [FractionallySizedBox (Flutter Widget of the Week)](https://www.youtube.com/watch?v=PEsY654EGZ0)
* [FractionallySizedBox Class](https://api.flutter.dev/flutter/widgets/FractionallySizedBox-class.html)

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
