
* [AspectRatio class](https://api.flutter.dev/flutter/widgets/AspectRatio-class.html):根据设置调整子元素child的宽高比，适合用于需要固定宽高比的场景。

<iframe width="560" height="315" src="https://www.youtube.com/embed/XcnP3_mO_Ms" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
const AspectRatio({
  Key key,
  @required double aspectRatio, // 设置child组件的宽高比，`aspectRatio:3/2`:宽高比例为`3:2`
  Widget child
})
```

* `AspectRatio` 会在布局条件允许的范围内尽可能的扩展。Widget的高度是由宽度和比率决定的，类似于`BoxFit.contain`，按照固定比率去尽可能的沾满区域。
* 如果在满足区域限制条件后依然无法找到可行的尺寸，`AspectRatio`会优先适应布局限制条件，而忽略所设置的比率。

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
        body: new Container(
          height: 200.0,
          child: new AspectRatio(
            aspectRatio: 1.5,// 比率是1.5 => W = H * 1.5,所以AspectRatio组件的尺寸为(300,200)
            child: new Container(
              color: Colors.green,
            ),
          ),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/50.png" width = "25%" height = "25%"/>
