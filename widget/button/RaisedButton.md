
[RaisedButton Class](https://api.flutter.dev/flutter/material/RaisedButton-class.html)

# 构造函数

## RaisedButton()

```dart
RaisedButton({
	Key key,
	@required VoidCallback onPressed,
	VoidCallback onLongPress,
	ValueChanged<bool> onHighlightChanged,
	ButtonTextTheme textTheme,
	Color textColor,// 文字颜色
	Color disabledTextColor,
	Color color, //按钮背景色
	Color disabledColor,
	Color focusColor,
	Color hoverColor,
	Color highlightColor,
	Color splashColor,
	Brightness colorBrightness,
	double elevation,
	double focusElevation,
	double hoverElevation,
	double highlightElevation,
	double disabledElevation,
	EdgeInsetsGeometry padding,
	VisualDensity visualDensity,
	ShapeBorder shape,
	Clip clipBehavior: Clip.none,
	FocusNode focusNode,
	bool autofocus: false,
	MaterialTapTargetSize materialTapTargetSize,
	Duration animationDuration,
	Widget child
})
```

## RaisedButton.icon()

```dart
RaisedButton.icon({
	Key key,
	@required VoidCallback onPressed,
	VoidCallback onLongPress,
	ValueChanged<bool> onHighlightChanged,
	ButtonTextTheme textTheme,
	Color textColor,
	Color disabledTextColor,
	Color color,
	Color disabledColor,
	Color focusColor,
	Color hoverColor,
	Color highlightColor,
	Color splashColor,
	Brightness colorBrightness,
	double elevation,
	double highlightElevation,
	double disabledElevation,
	ShapeBorder shape,
	Clip clipBehavior,
	FocusNode focusNode,
	bool autofocus,
	EdgeInsetsGeometry padding,
	MaterialTapTargetSize materialTapTargetSize,
	Duration animationDuration,
	@required Widget icon,
	@required Widget label
})
```