
* [BoxDecoration Class](https://api.flutter.dev/flutter/painting/BoxDecoration-class.html)

# 构造函数

```dart
const BoxDecoration({
	Color color,
	DecorationImage image,
	BoxBorder border,
	BorderRadiusGeometry borderRadius,
	List<BoxShadow> boxShadow,
	Gradient gradient,
	BlendMode backgroundBlendMode,
	BoxShape shape: BoxShape.rectangle
})
```

# 示例

## 边框

```dart
// 同时设置4条边框：1px粗细的黑色实线边框
BoxDecoration(
  border: Border.all(color: Colors.black, width: 1, style: BorderStyle.solid)
)

// 设置单边框：上边框为1px粗细的黑色实线边框，右边框为1px粗细的红色实线边框
BoxDecoration(
  border: Border(
    top: BorderSide(color: Colors.black, width: 1, style: BorderStyle.solid),
    right: BorderSide(color: Colors.red, width: 1, style: BorderStyle.solid),
  ),
)
```

## 阴影

```dart
BoxDecoration(
  boxShadow: [
    BoxShadow(
      offset: Offset(0, 0),
      blurRadius: 6,
      spreadRadius: 10,
      color: Color.fromARGB(20, 0, 0, 0),
    ),
  ],
)
```

## 渐变

```dart
// 从左到右，红色到蓝色的线性渐变
BoxDecoration(
  gradient: LinearGradient(
    begin: Alignment.centerLeft,
    end: Alignment.centerRight,
    colors: [Colors.red, Colors.blue],
  ),
)

// 从中心向四周扩散，红色到蓝色的径向渐变
BoxDecoration(
  gradient: RadialGradient(
    center: Alignment.center,
    colors: [Colors.red, Colors.blue],
  ),
)
```

## 圆角

```dart
// 同时设置4个角的圆角为5
BoxDecoration(
  borderRadius: BorderRadius.circular(5),
)

// 设置单圆角：左上角的圆角为5，右上角的圆角为10
BoxDecoration(
  borderRadius: BorderRadius.only(
    topLeft: Radius.circular(5),
    topRight: Radius.circular(10),
  ),
)
```