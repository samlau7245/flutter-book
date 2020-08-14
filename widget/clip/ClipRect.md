
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