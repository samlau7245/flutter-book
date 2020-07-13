
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
