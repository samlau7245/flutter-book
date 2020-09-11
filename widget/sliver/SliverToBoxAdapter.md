
[SliverToBoxAdapter-class](https://api.flutter.dev/flutter/widgets/SliverToBoxAdapter-class.html)

在使用`CustomScrollView`创建自定义滚动效果的时候，`CustomScrollView`只能包含`sliver`系列组件，如果包含普通的组件如何处理？使用`SliverToBoxAdapter`包裹。

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: CustomScrollView(
      slivers: [
        SliverAppBar(
          expandedHeight: 250,
          elevation: 0.0,
          flexibleSpace: FlexibleSpaceBar(
            background: Image.network(
              'http://img1.mukewang.com/5c18cf540001ac8206000338.jpg',
              fit: BoxFit.cover,
            ),
          ),
        ),
        SliverToBoxAdapter(
          child: Container(
            color: Colors.black45,
            height: 120.0,
          ),
        ),
        SliverList(
          delegate: SliverChildBuilderDelegate(
            (_, index) {
              return Container(
                height: 100.0,
                color: Colors.primaries[index % Colors.primaries.length],
                child: Center(
                  child: Text("$index"),
                ),
              );
            },
            childCount: 20,
          ),
        ),
      ],
    ),
  );
}
```

<img src="/assets/images/widgets/56.gif"/>