
# ConstrainedBox(限定最大最小宽度布局)
`ConstrainedBox`的作用就是限定子元素child的最大宽度、最大高度、最小宽度和最小高度。例如：通过`ConstrainedBox`来限制文本 Widget 的最大宽度，使其跨越多行。

* [ConstrainedBox (Flutter Widget of the Week)](https://www.youtube.com/watch?v=o2KveVr7adg)
* [CodePen-ConstrainedBox,搭配视频讲解看](https://codepen.io/samlau7245/pen/pojaGdO)
* [ConstrainedBox class](https://api.flutter.dev/flutter/widgets/ConstrainedBox-class.html)

| --- | --- | --- |
|constraints|BoxConstraints|添加到child上的额外限制条件，BoxConstraints的作用就是限制各种最大最小宽高|
|child|||

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
        body: new ConstrainedBox(
          constraints: const BoxConstraints(
            minWidth: 150.0,
            minHeight: 150.0,
            maxWidth: 220.0,
            maxHeight: 220.0,
          ),
          child: new Container(
            width: 300.0,
            height: 300.0,
            color: Colors.red,
          ),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/48.png" width = "25%" height = "25%"/>
