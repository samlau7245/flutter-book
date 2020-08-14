
[InteractiveViewer Class](https://api.flutter-io.cn/flutter/widgets/InteractiveViewer-class.html)

构建常见交互，如平移、缩放和拖放，甚至在可调节大小的窗口中也可实现这些交互。

<img src="/assets/images/widgets/32.gif"/>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ChFa0A72Uto" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
InteractiveViewer({
	Key key,
	bool alignPanAxis: false,
	EdgeInsets boundaryMargin: EdgeInsets.zero,
	bool constrained: true,
	double maxScale: 2.5,
	double minScale: 0.8,
	GestureScaleEndCallback onInteractionEnd,
	GestureScaleStartCallback onInteractionStart,
	GestureScaleUpdateCallback onInteractionUpdate,
	bool panEnabled: true,
	bool scaleEnabled: true,
	TransformationController transformationController,
	@required Widget child
})

TransformationController(
	[Matrix4 value]
)
```

# 资料

<img src="/assets/images/widgets/34.gif"/>

* [五子棋示例](https://github.com/justinmc/flutter-go)

<img src="/assets/images/widgets/33.gif"/>

* [知晓拖放操作的位置](https://github.com/monkeyswarm/DragTargetDetailsExample)