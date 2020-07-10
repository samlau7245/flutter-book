* [SizedBox class](https://api.flutter.dev/flutter/widgets/SizedBox-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/EHPu_DzRfqA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
const SizedBox({
  Key key,
  double width, // 如果具体设置了宽度，则强制child宽度为此值； 如果没有设置，则根据child宽度调整自身宽度,填充整个父类 Widget
  double height, // 如果具体设置了高度，则强制child高度为此值； 如果没有设置，则根据child高度调整自身宽度,填充整个父类 Widget
  Widget child
})

// 创建父类允许最大尺寸的约束Box
const SizedBox.expand({
  Key key,
  Widget child
})

// 创建指定大小的约束Box
SizedBox.fromSize({
  Key key,
  Widget child,
  Size size
})

// 创建父类允许最小尺寸的约束Box
const SizedBox.shrink({
  Key key,
  Widget child
})
```

# 示例

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(
          title: Text('data'),
        ),
        body: SizedBox(
          width: 200.0,
          height: 300.0,
          child: const Card(
            child: Text(
              'data',
              style: TextStyle(fontSize: 36.0),
            ),
          ),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/47.png"/>
