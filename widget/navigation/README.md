
# 导航监控

可以通过`MaterialApp.navigatorObservers`来监听用户操作导航的过程。

```dart
class LocalNavigatorObserver implements NavigatorObserver {
  @override
  void didPop(Object route, Route previousRoute) {}
  @override
  void didPush(Route route, Route previousRoute) {}
  @override
  void didRemove(Route route, Route previousRoute) {}
  @override
  void didReplace({Route newRoute, Route oldRoute}) {}
  @override
  void didStartUserGesture(Route route, Route previousRoute) {}
  @override
  void didStopUserGesture() {}
  @override
  NavigatorState get navigator => throw UnimplementedError();
}

class _TutorialAppState extends State<TutorialApp> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      navigatorObservers: [
        LocalNavigatorObserver(),
      ],
    );
  }
}
```