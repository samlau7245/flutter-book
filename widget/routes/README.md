
Flutter关于`Route`的系统库文件：

* `MaterialPageRoute`
* `ModalRoute`
* `OverlayRoute`
* `PageRoute`
* `PageRouteBuilder`
* `PopupRoute`
* `Route`
* `RouteAware`
* `RouteObserver`
* `RouteSettings`
* `RouteTransitionRecord`
* `TransitionRoute`
* `LocalHistoryRoute`
* `MaterialRouteTransitionMixin`
* `RoutePopDisposition`
* `InitialRouteListFactory`
* `PageRouteFactory`
* `RouteBuilder`
* `RouteFactory`
* `RouteListFactory`
* `RoutePageBuilder`
* `RoutePredicate`
* `RouteTransitionsBuilder`

# 基础用法

```dart
const MaterialApp({
  Map<String, WidgetBuilder> routes: const {},
  String initialRoute,
})
```

示例：

```dart
class _TutorialAppState extends State<TutorialApp> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      routes: _routesManager(),
    );
  }
  Map<String, WidgetBuilder> _routesManager() {
    return {
      "/": (_) => TutorialPage1(),
      "/page2": (_) => TutorialPage2(),
      "/page3": (_) => TutorialPage3(),
    };
  }
}
```

> **[warning] 使用注意**
>
> `MaterialApp.routes`中的路由`"/"`和`MaterialApp.home`不能同时使用，根页面只能选择一种实现方案。

## 给路由传参数

```dart
// 注册路由
routes:{
    "new_page":(context)=>EchoRoute(),
},

// 通过RouteSetting对象获取路由参数
class EchoRoute extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    //获取路由参数  
    var args=ModalRoute.of(context).settings.arguments
  }
}

// Navigator 跳转路由
Navigator.of(context).pushNamed("new_page", arguments: "hi");
```

# 动态路由

`MaterialApp`中可以通过`onGenerateRoute`来实现动态路由的功能。


```dart
const MaterialApp({
  Map<String, WidgetBuilder> routes: const {},
  String initialRoute,
  RouteFactory onGenerateRoute, // 动态路由
  InitialRouteListFactory onGenerateInitialRoutes,
  RouteFactory onUnknownRoute,
})

Route RouteFactory (
	RouteSettings settings
)

RouteSettings({
	String name, // 路由的名字，(e.g., "/settings")
	Object arguments // 路由的传参
})
```

示例:

```dart
class _TutorialAppState extends State<TutorialApp> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: TutorialPage1(),
      onGenerateRoute: generateRoute,
    );
  }

  Route generateRoute(RouteSettings routeSettings) {
    switch (routeSettings.name) {
      case '/page2':
        return MaterialPageRoute(
            builder: (_) => TutorialPage2(inputParams: routeSettings.arguments));
      case '/page3':
        return MaterialPageRoute(builder: (_) => TutorialPage3());
      default:
        return MaterialPageRoute(builder: (_) => TutorialPage1());
    }
  }
}
```

如何实现`page1->page2`

```dart
Navigator.of(context).pushNamed('/page2',arguments: 'para');
```

<img src="/assets/images/widgets/38.gif"/> 

# 未知路由兼容

```dart
const MaterialApp({
  RouteFactory onUnknownRoute, // 设置未发现的路由
})
```

示例：

```dart
class _TutorialAppState extends State<TutorialApp> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      onGenerateRoute: generateRoute,
      onUnknownRoute: (routeSettings) => MaterialPageRoute(builder: (_) => TutorialNotFoundPage()),
    );
  }
}
```

# 导航不使用BuildContext

在使用`Navigator`的时候需要传入`context`上下文参数，实现不需要传`context`直接导航的功能。

```dart
class NavigatorService {
  // 定义单例
  static final NavigatorService _instance = NavigatorService._internal();
  NavigatorService._internal();
  factory NavigatorService() {
    return _instance;
  }

  final GlobalKey<NavigatorState> navigatorKey = GlobalKey<NavigatorState>();

  Future<dynamic> pushTo(String routeName) {
    return navigatorKey.currentState.pushNamed(routeName, arguments: 'A');
  }

  void pop() {
    if (navigatorKey.currentState.canPop()) {
      navigatorKey.currentState.pop();
    }
  }
}
```

获取APP中的全局`Key`。

```dart
class _TutorialAppState extends State<TutorialApp> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: TutorialPage1(),
      onGenerateRoute: generateRoute,
      navigatorKey: NavigatorService().navigatorKey,
    );
  }

  Route generateRoute(RouteSettings routeSettings) {
    switch (routeSettings.name) {
      case '/page2':
        return MaterialPageRoute(builder: (_) => TutorialPage2(inputParams: routeSettings.arguments));
      case '/page3':
        return MaterialPageRoute(builder: (_) => TutorialPage3());
      default:
      return MaterialPageRoute(builder: (_) => TutorialPage1());
    }
  }
}
```

在具体的页面上进行页面`push`,因为这种方法不需要`BuildContext`，可以直接在Model层进行调用；基本实现了`V-M`分离。

```dart
NavigatorService().pushTo('/page2');
```

# 不定义路由直接跳转

```dart
class NavigatorUtil {
  static push(BuildContext context, Widget widget) async {
    final result = await Navigator.push(
        context, MaterialPageRoute(builder: (_) => widget));
    return result;
  }
}
```


















































