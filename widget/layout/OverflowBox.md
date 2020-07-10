
* [OverflowBox class](https://api.flutter.dev/flutter/widgets/OverflowBox-class.html)

# 构造函数

```dart
const OverflowBox({
  Key key,
  AlignmentGeometry alignment: Alignment.center,
  double minWidth, // 允许 child 的最小宽度。如果 child 宽度小于这个值，则按照最小宽度进行显示
  double maxWidth, // 允许 child 的最大宽度。如果 child 宽度大于这个值，则按照最大宽度进行显示
  double minHeight, // 允许 child 的最小高度。如果 child 宽度小于这个值，则按照最小高度进行显示
  double maxHeight, // 允许 child 的最大高度。如果 child 宽度大于这个值，则按照最大高度进行显示
  Widget child
})
```

* 当`OverflowBox`的最大尺寸大于`child`的时候，`child`可以完整显示。
* 当`OverflowBox`的最大尺寸小于`child`的时候，则以最大尺寸为基准，当然这个尺寸是可以突破父节点的。

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
