
[ListWheelScrollView-class](https://api.flutter.dev/flutter/widgets/ListWheelScrollView-class.html)

# 构造函数

```dart
ListWheelScrollView({
	Key key, 
	@required double itemExtent, 指定每一个Item的高度
	@required List<Widget> children

	ScrollController controller, 
	ScrollPhysics physics, 
	Clip clipBehavior: Clip.hardEdge, 
	
	double diameterRatio: RenderListWheelViewport.defaultDiameterRatio, 
	double perspective: RenderListWheelViewport.defaultPerspective, 
	double offAxisFraction: 0.0, 
	double magnification: 1.0, 
	double overAndUnderCenterOpacity: 1.0, 
	double squeeze: 1.0, 
	
	ValueChanged<int> onSelectedItemChanged, 
	
	bool useMagnifier: false, 
	bool renderChildrenOutsideViewport: false, 
})

ListWheelScrollView.useDelegate({
	Key key, 
	@required double itemExtent, 
	@required ListWheelChildDelegate childDelegate

	ScrollController controller, 
	ScrollPhysics physics, 
	Clip clipBehavior: Clip.hardEdge, 

	double diameterRatio: RenderListWheelViewport.defaultDiameterRatio, 设置滚轮的直径距离，diameterRatio越小表示圆筒越圆,默认值是2
	double perspective: RenderListWheelViewport.defaultPerspective, 
	double offAxisFraction: 0.0, 
	double overAndUnderCenterOpacity: 1.0, 
	double squeeze: 1.0, 

	ValueChanged<int> onSelectedItemChanged, 

	bool renderChildrenOutsideViewport: false, 

	double magnification: 1.0, // 放大倍数
	bool useMagnifier: false,  // 是否启动放大镜

})
```

# 示例

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: ListWheelScrollView.useDelegate(
      itemExtent: 150,
      childDelegate: ListWheelChildBuilderDelegate(
        builder: (_, index) {
          return Container(
            color: Colors.primaries[index % 10],
            child: Center(child: Text("Index $index")),
          );
        },
        childCount: 20,
      ),
    ),
  );
}
```

<img src="/assets/images/widgets/60.gif"/>
