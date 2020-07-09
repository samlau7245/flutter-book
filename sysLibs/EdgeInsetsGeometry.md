
* [EdgeInsets Class](https://api.flutter.dev/flutter/painting/EdgeInsets-class.html)
* [EdgeInsetsDirectional Class](https://api.flutter.dev/flutter/painting/EdgeInsetsDirectional-class.html)
* [EdgeInsetsGeometry Class](https://api.flutter.dev/flutter/painting/EdgeInsetsGeometry-class.html)

这三个类的继承关系为：

* `Object`
	* `EdgeInsetsGeometry`
		* `EdgeInsets`
		* `EdgeInsetsDirectional`

# EdgeInsetsGeometry

# EdgeInsets

## 构造函数

```dart
// 所有方向
const EdgeInsets.all(double value)
// 分别定义各个方向的边框
const EdgeInsets.only({double left: 0.0,double top: 0.0,double right: 0.0,double bottom: 0.0})
// 自定义垂直、水平方向
const EdgeInsets.symmetric({double vertical: 0.0,double horizontal: 0.0})
// 根据机型屏幕尺寸定义
EdgeInsets.fromWindowPadding(ui.WindowPadding padding, double devicePixelRatio)
const EdgeInsets.fromLTRB(double left, double top, double right, double bottom)
```

# EdgeInsetsDirectional

## 构造函数

```dart
const EdgeInsetsDirectional.fromSTEB(double start, double top, double end, double bottom)
const EdgeInsetsDirectional.only({double start: 0.0, double top: 0.0, double end: 0.0, double bottom: 0.0})
```

