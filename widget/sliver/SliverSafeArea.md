
[SliverSafeArea-class](https://api.flutter.dev/flutter/widgets/SliverSafeArea-class.html)

# 构造函数

```dart
const SliverSafeArea({
	Key key,
	@required Widget sliver
	bool left: true,
	bool top: true,
	bool right: true,
	bool bottom: true,
	EdgeInsets minimum: EdgeInsets.zero,
})
```

```dart
@override
Widget build(BuildContext context) {
  return CustomScrollView(
    slivers: [
      SliverGrid(
        delegate: SliverChildBuilderDelegate(
          (_, index) {
            return Container(
              color: Colors.primaries[index % Colors.primaries.length],
            );
          },
          childCount: 10,
        ),
        gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: 3,
          mainAxisSpacing: 5,
          crossAxisSpacing: 5,
        ),
      ),
    ],
  );
}
```

<img src="/assets/images/widgets/45.png"/>

```dart
@override
Widget build(BuildContext context) {
  return CustomScrollView(
    slivers: [
      SliverSafeArea(
        sliver: SliverGrid(
          delegate: SliverChildBuilderDelegate(
            (_, index) {
              return Container(
                color: Colors.primaries[index % Colors.primaries.length],
              );
            },
            childCount: 10,
          ),
          gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
            crossAxisCount: 3,
            mainAxisSpacing: 5,
            crossAxisSpacing: 5,
          ),
        ),
      ),
    ],
  );
}
```

<img src="/assets/images/widgets/46.gif"/>

添加了`SliverSafeArea`以后可以发现，顶部导航栏添加了安全间距。

