
# AspectRatio(调整宽高比)

`AspectRatio` 作用是根据设置调整子元素child的宽高比，适合用于需要固定宽高比的场景。

* [AspectRatio Class](https://api.flutter.dev/flutter/widgets/AspectRatio-class.html)

使用`AspectRatio`进行布局的情况：

* `AspectRatio` 会在布局条件允许的范围内尽可能的扩展。Widget的高度是由宽度和比率决定的，类似于`BoxFit.contain`，按照固定比率去尽可能的沾满区域。
* 如果在满足所欲呕限制条件后依然无法找到可行的尺寸，`AspectRatio`会优先适应布局限制条件，而忽略所设置的比率。

|属性|类型|描述|
| --- | --- | --- |
|aspectRatio|double|设置child组件的宽高比，`aspectRatio:3/2`:宽高比例为`3:2`|
|child|Widget||

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
