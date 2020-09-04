
[Material Class](https://api.flutter.dev/flutter/material/Material-class.html)

`Material`组件帮助开发者实现[Material Design](https://material.io/design)。

# 构造函数

```dart
const Material({
	Key key,
	MaterialType type: MaterialType.canvas,
	double elevation: 0.0,
	Color color,
	Color shadowColor: const Color(0xFF000000),
	TextStyle textStyle,
	BorderRadiusGeometry borderRadius,
	ShapeBorder shape,
	bool borderOnForeground: true,
	Clip clipBehavior: Clip.none,
	Duration animationDuration: kThemeChangeDuration,
	Widget child
})

enum MaterialType {
  canvas,
  card,
  circle,
  button,
  transparency
}
```