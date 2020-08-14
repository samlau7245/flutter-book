
[WillPopScope Class](https://api.flutter.dev/flutter/widgets/WillPopScope-class.html)

以下几种情况我们会用到`WillPopScope`：

* 需要询问用户是否退出。
* App中有多个`Navigator`，想要的是让其中一个`Navigator 退出`，而不是直接让在Widget tree 底层的`Navigator`退出。

# 构造函数

```dart
const WillPopScope({
	Key key,
	@required Widget child,
	@required WillPopCallback onWillPop
})
```