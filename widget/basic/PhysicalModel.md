
[PhysicalModel Class](https://api.flutter.dev/flutter/widgets/PhysicalModel-class.html)

# 构造函数

```dart
PhysicalModel({
	Key key, 
	BoxShape shape: BoxShape.rectangle, 
	Clip clipBehavior: Clip.none, 
	BorderRadius borderRadius, 
	double elevation: 0.0, 
	@required Color color, 
	Color shadowColor: const Color(0xFF000000), 
	Widget child
})
```

# 示例

```dart
Widget build(BuildContext context) {
  return PhysicalModel(
    color: Colors.transparent,
    borderRadius: BorderRadius.circular(6),
    clipBehavior: Clip.antiAlias,
    child: Column(
      children: _gridNaviItems(context),
    ),
  );
}
```

<img src="/assets/images/widgets/37.png"/>