
* [AutomaticKeepAliveClientMixin](https://api.flutter.dev/flutter/widgets/AutomaticKeepAliveClientMixin-mixin.html)
* [AutomaticKeepAlive Class](https://api.flutter.dev/flutter/widgets/AutomaticKeepAlive-class.html)
* [KeepAliveNotification Class](https://api.flutter.dev/flutter/widgets/KeepAliveNotification-class.html)

当通过设置`wantKeepAlive`属性为`true`，则当前页面回保持激活状态。

```dart
const AutomaticKeepAlive({
	Key key,
	Widget child
})

const KeepAliveNotification(
	Listenable handle
)
```

# 示例

```dart
class _HomePageState with AutomaticKeepAliveClientMixin{//要点1
  @override
  bool get wantKeepAlive => true;//要点2

  Widget build(BuildContext context){
    super.build(context);//要点3
  }
}
```