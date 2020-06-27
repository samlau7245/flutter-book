
# OverflowBox 溢出父容器显示
`OverflowBox` 组件运行子元素`child`超出父容器的显示范围。

* 当`OverflowBox`的最大尺寸大于`child`的时候，`child`可以完整显示。
* 当`OverflowBox`的最大尺寸小于`child`的时候，则以最大尺寸为基准，当然这个尺寸是可以突破父节点的。

|属性|类型|描述|
| --- | --- | --- |
|alignment|AlignmentGeometry||
|minWidth|double|允许 child 的最小宽度。如果 child 宽度小于这个值，则按照最小宽度进行显示|
|maxWidth|double|允许 child 的最大宽度。如果 child 宽度大于这个值，则按照最大宽度进行显示|
|minHeight|double|允许 child 的最小高度。如果 child 宽度小于这个值，则按照最小高度进行显示|
|maxHeight|double|允许 child 的最小高度。如果 child 宽度小于这个值，则按照最小高度进行显示|

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
          width: 200.0,
          height: 200.0,
          padding: const EdgeInsets.all(10.0),
          child: OverflowBox(
            alignment: Alignment.topLeft,
            maxWidth: 300.0,
            maxHeight: 500.0,
            child: Container(
              color: Colors.green,
              width: 400.0,
              height: 400.0,
            ),
          ),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/46.png" width = "25%" height = "25%"/>
