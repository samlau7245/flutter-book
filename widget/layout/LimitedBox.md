
# LimitedBox(限定最大宽高布局)

`LimitedBox`和`ConstrainedBox`组件类似。只不过`LimitedBox`没有最小宽高限制。

|属性|类型|描述|
| --- | --- | --- |
|maxWidth|double|最大宽度|
|maxHeight|double|最大高度|

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

// 宽度300的Container上添加一个约束最大最小宽高的ConstrainedBox。
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(
          title: Text('data'),
        ),
        body: Row(
          children: <Widget>[
            Container(
              color: Colors.red,
              width: 100.0,
            ),
            LimitedBox(
              maxWidth: 100.0,
              child: Container(
                color: Colors.blue,
                width: 250.0,// 虽然设置了25.0 但是父容器限制了最大宽度
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/49.png" width = "25%" height = "25%"/>
