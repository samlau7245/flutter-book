
* [LimitedBox class](https://api.flutter.dev/flutter/widgets/LimitedBox-class.html) : 限定最大宽高布局

<iframe width="560" height="315" src="https://www.youtube.com/embed/uVki2CIzBTs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
const LimitedBox({
  Key key,
  double maxWidth: double.infinity, // 最大宽度
  double maxHeight: double.infinity, // 最大高度
  Widget child
})
```

# 示例

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
