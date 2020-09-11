
[NestedScrollView](https://api.flutter.dev/flutter/widgets/NestedScrollView-class.html)

# 构造函数

```dart
const NestedScrollView({
	Key key,
	ScrollController controller,
	Axis scrollDirection: Axis.vertical,
	bool reverse: false,
	ScrollPhysics physics,
	@required NestedScrollViewHeaderSliversBuilder headerSliverBuilder,
	@required Widget body,
	DragStartBehavior dragStartBehavior: DragStartBehavior.start,
	bool floatHeaderSlivers: false,
	Clip clipBehavior: Clip.hardEdge
})
```

# 示例

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: NestedScrollView(
      headerSliverBuilder: (BuildContext context, bool innerBoxIsScrolled) {
        return [
          SliverAppBar(
            elevation: 0.0,
            expandedHeight: 230,
            flexibleSpace: FlexibleSpaceBar(
              background: Image.network(
                'http://img1.mukewang.com/5c18cf540001ac8206000338.jpg',
                fit: BoxFit.fitHeight,
              ),
            ),
          ),
        ];
      },
      body: ListView.builder(
        itemBuilder: (_, index) {
          return Container(
            height: 80,
            child: Center(child: Text("Index$index")),
            color: Colors.primaries[index % Colors.primaries.length],
          );
        },
        itemCount: 20,
      ),
    ),
  );
}
```

<img src="/assets/images/widgets/61.gif"/>

