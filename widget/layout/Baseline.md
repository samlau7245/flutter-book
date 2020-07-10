
* [Baseline class](https://api.flutter.dev/flutter/widgets/Baseline-class.html):根据 child 的基线来放置 child 的 widgets。

# 构造函数

```dart
const Baseline({
	Key key,
	@required double baseline,
	@required TextBaseline baselineType,
	Widget child
})

enum TextBaseline {
  alphabetic, // 对齐字符底部的水平线
  ideographic, // 对齐表意字符串的水平线
}
```

# Baseline(基准线布局)

`Baseline` 将左右元素底部放到同一条水平线上。

* [Baseline Class](https://api.flutter.dev/flutter/widgets/Baseline-class.html)

<img src="/assets/images/flutter/54.png"/>
