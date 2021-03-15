
* Page
* Router
	* RouterDelegate 路由代理，定义应用程序中的路由行为。主要的工作就是监听 RouteInformationParser 和应用状态并通过当前页面列表构建。
	* RouteInformationParser

* `PopNavigatorRouterDelegateMixin`: 主要作用是响应 Android 设备的回退按钮。
* `ChangeNotifier`:  主要作用是事件通知。
* `RouteInformationParser`: 解析我们定义的数据类型。

```dart
Router({
	Key key, 
    RouteInformationProvider routeInformationProvider, 
    RouteInformationParser<T> routeInformationParser, 
    @required RouterDelegate<T> routerDelegate, 
    BackButtonDispatcher backButtonDispatcher
})
```

RouterDelegate

```
// RouterDelegate 继承了 Listenable ，它可以实现实时监听对象的状态。
abstract class RouterDelegate<T> extends Listenable{}
```

```dart
build(BuildContext context) → Widget
popRoute() → Future<bool>
setInitialRoutePath(T configuration) → Future<void>
setNewRoutePath(T configuration) → Future<void>
```

```dart
// @see https://api.flutter.dev/flutter/widgets/RouterDelegate/setNewRoutePath.html
@override
Future<void> setNewRoutePath(configuration) {
  throw UnimplementedError();
}
```


```dart
class Navigator2RouteDelegate extends RouterDelegate<String> {
  @override
  Widget build(BuildContext context) {
    return Navigator(
      pages: [],
      onPopPage: _onPopPage,
    );
  }
  ...
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(
      routerDelegate: delegate,
      title: 'Flutter Demo',
    );
  }
}
```

当`RouterDelegate`对象传入`MaterialApp.router()`构造函数后，`RouterDelegate.build`中的`Navigator`就成为了`Router`的子组件了。



* [Flutter Navigator2.0 完全指南与原理解析](https://mp.weixin.qq.com/s/hDLxWJuUylw8UaOidUa3Hg)
* [RouterDelegate class](https://api.flutter.dev/flutter/widgets/RouterDelegate-class.html)
* [Navigator 2.0 and Router 官方公开分享](https://docs.google.com/document/d/1Q0jx0l4-xymph9O6zLaOY4d_f7YFpNWX_eGbzYxr9wY/edit#)

* MaterialPageRoute()
* MaterialApp()
* Material()
* Scaffold()
* MaterialPage()






