
# FittedBox(缩放布局)

* [FittedBox (Flutter Widget of the Week)](https://youtu.be/T4Uehk3_wlY)
* [FittedBox-官方文档](https://api.flutter.dev/flutter/widgets/FittedBox-class.html)

FittedBox(缩放布局) 组件主要做两件事，`缩放(Scale)`和`位置调整(Position)`。

FittedBox会在自己的尺寸范围内缩放并且调整child的位置。使child适合其尺寸。有点像`ImageView`组件，`ImageView`会将图片在其范围内按照规则进行缩放位置调整。

布局行为分为两种情况:

* 如果外部有约束的话，按照外部约束调整自身尺寸，然后缩放调整child，按照指定的条件进行布局。
* 如果没有外部约束条件，则跟着child尺寸一致，指定的缩放以及位置属性将不起作用。

属性：

* 属性`alignment`：设置对齐方式，默认是`Alignment.center`，居中展示child。
* 属性`fit`：缩放方式。

|`fit`缩放属性|图解|描述|
| --- | --- | --- |
|contain|<img src="/assets/images/flutter/36.png"/>|`child`在`FittedBox`范围内尽可能大，但是不能超出其尺寸。【`contain`是在保持着`child`宽高比不变的大前提下尽可能的填满，一般是宽度或者高度达到最大值时就会停止缩放。】|
|cover|<img src="/assets/images/flutter/37.png"/>|按照原始尺寸填充整个容器，内容可能会超过容器范围|
|fill|<img src="/assets/images/flutter/38.png"/>|不按照宽高比填充，直接填满但是不会超过容器范围|
|fitHeight|<img src="/assets/images/flutter/39.png"/>|按照高度填充整个容器|
|fitWidth|<img src="/assets/images/flutter/40.png"/>|按照宽度填充整个容器|
|none|<img src="/assets/images/flutter/41.png"/>|没有任何填充|
|scaleDown|<img src="/assets/images/flutter/42.png"/>|根据情况缩小范围，内容不会超过容器范围，有时和`contain`一样有时和`none`一样|

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(title: Text('data'),),
        body: new Container(
          color: Colors.red,
          width: 200.0,
          height: 200.0,
          child: new FittedBox(
            fit: BoxFit.scaleDown,
            alignment: Alignment.topLeft,
            child: new Container(
              color: Colors.green,
              child: new Text('Test'),
            ),
          ),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/35.png" width = "25%" height = "25%"/>