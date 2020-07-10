
* [BoxConstraints Class](https://api.flutter.dev/flutter/rendering/BoxConstraints-class.html)

# 构造函数

```dart
// 用指定的约束大小创建框架大小
const BoxConstraints({
	double minWidth: 0.0,
	double maxWidth: double.infinity,
	double minHeight: 0.0,
	double maxHeight: double.infinity
})

// 创建扩展为填充另一个框约束的框约束
const BoxConstraints.expand({
	double width,
	double height
})

// 创建禁止大小大于给定大小的框约束
BoxConstraints.loose(
	Size size
)

// 仅用指定大小创建框大小
BoxConstraints.tight(
	Size size
)

// 用指定的约束大小创建框大小
const BoxConstraints.tightFor({
	double width,
	double height
})

// 创建需要给定宽度或高度的框约束，除非它们是无限的
const BoxConstraints.tightForFinite({
	double width: double.infinity,
	double height: double.infinity
})
```