
[ClipRect Class](https://api.flutter.dev/flutter/widgets/ClipRect-class.html)

默认情况下，`ClipRect`会阻止子`widget`在其边界外绘画，通常与`ClipRect`结合使用的`widget`：

* `CustomPaint`
* `CustomSingleChildLayout`
* `CustomMultiChildLayout`
* `Align`
* `OverflowBox`
* `SizedOverflowBox`

# 构造函数

```dart
const ClipRect({
Key key,
CustomClipper<Rect> clipper,
Clip clipBehavior: Clip.hardEdge,
Widget child
})
```

## 裁剪模式

```
enum Clip {
  none, // 无模式
  hardEdge, // 裁剪速度稍快，但容易失真，有锯齿
  antiAlias, // 裁剪边缘抗锯齿，使得裁剪更平滑，这种模式裁剪速度比 antiAliasWithSaveLayer 快，但是比 hardEdge 慢,该模式常用于圆形和弧形之类的形状裁剪
  antiAliasWithSaveLayer, // 裁剪后具有抗锯齿特性并分配屏幕缓冲区，所有后续操作在缓冲区进行，然后再进行裁剪和合成
}
```