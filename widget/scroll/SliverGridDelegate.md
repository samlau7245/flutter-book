
* [SliverGridDelegate Class](https://api.flutter.dev/flutter/rendering/SliverGridDelegate-class.html) 抽象类。
* [SliverGridDelegateWithFixedCrossAxisCount Class](https://api.flutter.dev/flutter/rendering/SliverGridDelegateWithFixedCrossAxisCount-class.html) 横轴为固定数量子元素的布局算法
* [SliverGridDelegateWithMaxCrossAxisExtent Class](https://api.flutter.dev/flutter/rendering/SliverGridDelegateWithMaxCrossAxisExtent-class.html) 横轴子元素为固定最大长度的布局算法

# 构造函数

```dart
const SliverGridDelegateWithFixedCrossAxisCount({
	@required int crossAxisCount, // 主向子元素的总数
	double mainAxisSpacing: 0.0, // 主轴方向的间距
	double crossAxisSpacing: 0.0, // 次轴方向子元素的间距
	double childAspectRatio: 1.0 // 子元素的宽高比
})

const SliverGridDelegateWithMaxCrossAxisExtent({
	@required double maxCrossAxisExtent, // 子元素在主轴上的最大长度
	double mainAxisSpacing: 0.0, // 主轴方向的间距
	double crossAxisSpacing: 0.0, // 次轴方向子元素的间距
	double childAspectRatio: 1.0 // 子元素的宽高比
})
```

<img src="/assets/images/widgets/35.png"/>
