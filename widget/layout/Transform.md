
# Transform(矩阵转换)

* [Transform (Flutter Widget of the Week)](https://www.youtube.com/watch?v=9z_YNlRlWfA)

`Transform` 主要作用就是做矩阵转换。对组件进行平移、旋转和缩放的等操作。

```dart
const Transform({
  Key key,
  @required this.transform,
  this.origin,
  this.alignment,
  this.transformHitTests = true,
  Widget child,
});
```

|属性|类型|描述|
| --- | --- | --- |
|transform|Matrix4|一个4x4的矩阵。|
|origin|Offset|旋转点，相对于左上角顶点的偏移。默认旋转点是在左上角顶点|
|alignment|AlignmentGeometry|对齐方式|
|transformHitTests|bool|点击区域石佛业做相应的改变|

```dart
Transform.translate({Key key,@required Offset offset,this.transformHitTests = true,Widget child,});
```
