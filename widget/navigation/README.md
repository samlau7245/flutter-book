
* [BottomNavigationBar](https://api.flutter.dev/flutter/material/BottomNavigationBar-class.html)
* [BottomNavigationBarItem](https://api.flutter.dev/flutter/material/BottomNavigationBarItem-class.html)
* [BottomNavigationBarTheme](https://api.flutter.dev/flutter/material/BottomNavigationBarTheme-class.html)
* [BottomNavigationBarThemeData](https://api.flutter.dev/flutter/material/BottomNavigationBarThemeData-class.html)
* [NavigationRail](https://api.flutter.dev/flutter/material/NavigationRail-class.html)
* [NavigationRailDestination](https://api.flutter.dev/flutter/material/NavigationRailDestination-class.html)
* [NavigationRailTheme](https://api.flutter.dev/flutter/material/NavigationRailTheme-class.html)
* [NavigationRailThemeData](https://api.flutter.dev/flutter/material/NavigationRailThemeData-class.html)
* [NavigationToolbar](https://api.flutter.dev/flutter/material/NavigationToolbar-class.html)
* [Navigator](https://api.flutter.dev/flutter/material/Navigator-class.html)
* [NavigatorObserver](https://api.flutter.dev/flutter/material/NavigatorObserver-class.html)
* [NavigatorState](https://api.flutter.dev/flutter/material/NavigatorState-class.html)

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