
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

# Navigator 2.0

* **Page** 用来表示 `Navigator` 路由栈中各个页面的配置信息。
* **Router** 用来制定要由 `Navigator` 展示的页面列表，通常，该页面列表会根据系统或应用程序的状态改变而改变。
* **RouteInformationParser** 持有 `RouteInformationProvider` 提供的 `RouteInformation` ，可以将其解析为我们定义的数据类型。
* **RouterDelegate** 定义应用程序中的路由行为，例如 Router 如何知道应用程序状态的变化以及如何响应。主要的工作就是监听 `RouteInformationParser` 和应用状态并通过当前页面列表构建。
* **BackButtonDispatcher** 响应后退按钮，并通知 `Router`。

<img src="/assets/images/widget/navigator/01.png"/>
































































