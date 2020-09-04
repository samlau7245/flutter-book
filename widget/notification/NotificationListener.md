
通过实现`NotificationListener`来监听Widget的树结构。

[NotificationListener Class](https://api.flutter.dev/flutter/widgets/NotificationListener-class.html)

# 构造函数

```dart
const NotificationListener<T extends Notification>({
	Key key,
	@required Widget child,
	NotificationListenerCallback<T> onNotification
})
```

# 示例

动态监听`ListView`滚动：

```dart
RefreshIndicator(
 onRefresh: _handleRefresh,
 child: NotificationListener(
   onNotification: (Notification notification) {
     if (notification is ScrollNotification &&
         notification.depth == 0) {
       _onScroll(notification.metrics.pixels);
     }
     return false;
   },
   child: _listView(),
 ),
```