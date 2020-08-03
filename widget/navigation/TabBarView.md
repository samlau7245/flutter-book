
[TabBarView Class](https://api.flutter.dev/flutter/material/TabBarView-class.html)

# 构造函数

```dart
const TabBarView({
	Key key,
	@required List<Widget> children,
	TabController controller, // 如果 TabController 没有提供，那默认会使用 DefaultTabController
	ScrollPhysics physics, // // 列表滚动至边缘后继续拖动的物理效果，Android与iOS效果不同。
	DragStartBehavior dragStartBehavior: DragStartBehavior.start
})
```

> 使用 `TabBarView` 是有条件要求的，`TabBarView` 的父 `Widget` 必须知道宽高才能布局，但是一般我们在实际项目使用的时候又不会写死宽高，因此一般我都会在一个 `Expanded` 中使用 `TabBarView`。