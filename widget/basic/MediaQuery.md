
# MediaQuery

[MediaQuery Class](https://api.flutter.dev/flutter/widgets/MediaQuery-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/A3WrA4zAaPw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 构造函数

```dart
MediaQuery({
	Key key, 
	@required MediaQueryData data, 
	@required Widget child
})

MediaQuery.removePadding({
	Key key, 
	@required BuildContext context, 
	bool removeLeft: false, 
	bool removeTop: false, 
	bool removeRight: false, 
	bool removeBottom: false, 
	@required Widget child
})

MediaQuery.removeViewInsets({
	Key key, 
	@required BuildContext context, 
	bool removeLeft: false, 
	bool removeTop: false, 
	bool removeRight: false, 
	bool removeBottom: false, 
	@required Widget child
})

MediaQuery.removeViewPadding({
	Key key, 
	@required BuildContext context, 
	bool removeLeft: false, 
	bool removeTop: false, 
	bool removeRight: false, 
	bool removeBottom: false, 
	@required Widget child
})
```

> **[danger]**
>
> 使用MediaQuery必须要MaterialApp 或者WidgetsApp 去包裹我们的Widget，这样才能够提供正常使用它，否则会出现错误

## 静态方法

```dart
bool boldTextOverride(BuildContext context);
MediaQueryData of(BuildContext context, {bool nullOk: false});
Brightness platformBrightnessOf(BuildContext context);
double textScaleFactorOf(BuildContext context);
```

# MediaQueryData

## 构造函数

```dart
MediaQueryData({
	Size size: Size.zero, 
	double devicePixelRatio: 1.0, 
	double textScaleFactor: 1.0, 
	Brightness platformBrightness: Brightness.light, 
	EdgeInsets padding: EdgeInsets.zero, 
	EdgeInsets viewInsets: EdgeInsets.zero, 
	EdgeInsets systemGestureInsets: EdgeInsets.zero, 
	EdgeInsets viewPadding: EdgeInsets.zero, 
	bool alwaysUse24HourFormat: false, 
	bool accessibleNavigation: false, 
	bool invertColors: false, 
	bool highContrast: false, 
	bool disableAnimations: false, 
	bool boldText: false, 
	NavigationMode navigationMode: NavigationMode.traditional
})

MediaQueryData.fromWindow(Window window)
```

## 属性

```dart
bool accessibleNavigation;
bool alwaysUse24HourFormat;
bool boldText;
double devicePixelRatio;
bool disableAnimations;
int hashCode;
bool highContrast;
bool invertColors;
NavigationMode navigationMode;
Orientation orientation;
EdgeInsets padding;
Brightness platformBrightness;
Type runtimeType;
Size size;  //返回context所在的窗口Size
EdgeInsets systemGestureInsets;
double textScaleFactor;
EdgeInsets viewInsets;
EdgeInsets viewPadding;
```