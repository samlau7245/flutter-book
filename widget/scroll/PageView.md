
[PageView Class](https://api.flutter.dev/flutter/widgets/PageView-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/J1gE9xvph-A" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
PageView({
	Key key, 
	Axis scrollDirection: Axis.horizontal, 
	bool reverse: false, 
	PageController controller, 
	ScrollPhysics physics, 
	bool pageSnapping: true, 
	ValueChanged<int> onPageChanged, 
	List<Widget> children: const [], 
	DragStartBehavior dragStartBehavior: DragStartBehavior.start, 
	bool allowImplicitScrolling: false
})

PageView.builder({
	Key key, 
	Axis scrollDirection: Axis.horizontal, 
	bool reverse: false, 
	PageController controller, 
	ScrollPhysics physics, 
	bool pageSnapping: true, 
	ValueChanged<int> onPageChanged, 
	@required IndexedWidgetBuilder itemBuilder, 
	int itemCount, 
	DragStartBehavior dragStartBehavior: DragStartBehavior.start, 
	bool allowImplicitScrolling: false
})

PageView.custom({
	Key key, 
	Axis scrollDirection: Axis.horizontal, 
	bool reverse: false, 
	PageController controller, 
	ScrollPhysics physics, 
	bool pageSnapping: true, 
	ValueChanged<int> onPageChanged, 
	@required SliverChildDelegate childrenDelegate, 
	DragStartBehavior dragStartBehavior: DragStartBehavior.start, 
	bool allowImplicitScrolling: false
})
```