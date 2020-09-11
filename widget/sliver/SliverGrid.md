
* [SliverGrid-class](https://api.flutter.dev/flutter/widgets/SliverGrid-class.html)
* [SliverChildDelegate-class](https://api.flutter.dev/flutter/widgets/SliverChildDelegate-class.html)
	* [SliverChildBuilderDelegate-class](https://api.flutter.dev/flutter/widgets/SliverChildBuilderDelegate-class.html)
	* [SliverChildListDelegate-class](https://api.flutter.dev/flutter/widgets/SliverChildListDelegate-class.html)
* [SliverGridDelegate-class](https://api.flutter.dev/flutter/rendering/SliverGridDelegate-class.html)
	* [SliverGridDelegateWithFixedCrossAxisCount](https://api.flutter.dev/flutter/rendering/SliverGridDelegateWithFixedCrossAxisCount-class.html)
	* [SliverGridDelegateWithMaxCrossAxisExtent](https://api.flutter.dev/flutter/rendering/SliverGridDelegateWithMaxCrossAxisExtent-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/ORiTTaVY6mM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

## SliverGrid

```dart
SliverGrid({
	Key key, 
	@required SliverChildDelegate delegate, 
	@required SliverGridDelegate gridDelegate
})

SliverGrid.count({
	Key key, 
	@required int crossAxisCount, 
	double mainAxisSpacing: 0.0, 
	double crossAxisSpacing: 0.0, 
	double childAspectRatio: 1.0, 
	List<Widget> children: const []
})

SliverGrid.extent({
	Key key, 
	@required double maxCrossAxisExtent, 
	double mainAxisSpacing: 0.0, 
	double crossAxisSpacing: 0.0, 
	double childAspectRatio: 1.0, 
	List<Widget> children: const []
})
```

## SliverChildDelegate

### SliverChildBuilderDelegate

```dart
const SliverChildBuilderDelegate( 
	IndexedWidgetBuilder builder, // 子控件构建器
	{ChildIndexGetter findChildIndexCallback,
	int childCount, // 子控件总数
	bool addAutomaticKeepAlives: true,
	bool addRepaintBoundaries: true,
	bool addSemanticIndexes: true,
	SemanticIndexCallback semanticIndexCallback: _kDefaultSemanticIndexCallback,
	int semanticIndexOffset: 0
})

Widget IndexedWidgetBuilder (BuildContext context,int index);
```

### SliverChildListDelegate

```dart
SliverChildListDelegate(List<Widget> children, 
	{bool addAutomaticKeepAlives: true, 
	bool addRepaintBoundaries: true, 
	bool addSemanticIndexes: true, 
	SemanticIndexCallback semanticIndexCallback: _kDefaultSemanticIndexCallback, 
	int semanticIndexOffset: 0
})

SliverChildListDelegate.fixed(List<Widget> children, 
	{bool addAutomaticKeepAlives: true, 
	bool addRepaintBoundaries: true, 
	bool addSemanticIndexes: true, 
	SemanticIndexCallback semanticIndexCallback: _kDefaultSemanticIndexCallback, 
	int semanticIndexOffset: 0
})
```

## SliverGridDelegate

### SliverGridDelegateWithFixedCrossAxisCount

```dart
const SliverGridDelegateWithFixedCrossAxisCount({
	@required int crossAxisCount, // 主向子元素的总数
	double mainAxisSpacing: 0.0, // 主轴方向的间距
	double crossAxisSpacing: 0.0, // 次轴方向子元素的间距
	double childAspectRatio: 1.0 // 子元素的宽高比
})
```

### SliverGridDelegateWithMaxCrossAxisExtent

```dart
const SliverGridDelegateWithMaxCrossAxisExtent({
	@required double maxCrossAxisExtent, // 子元素在主轴上的最大长度
	double mainAxisSpacing: 0.0, // 主轴方向的间距
	double crossAxisSpacing: 0.0, // 次轴方向子元素的间距
	double childAspectRatio: 1.0 // 子元素的宽高比
})
```

<img src="/assets/images/widgets/35.png"/>

# 示例

```dart
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

