
# 构造方法

```dart
const Navigator({
	Key key,
	List<Page> pages: const >[],
	PopPageCallback onPopPage,
	String initialRoute,
	RouteListFactory onGenerateInitialRoutes: Navigator.defaultGenerateInitialRoutes,
	RouteFactory onGenerateRoute,
	RouteFactory onUnknownRoute,
	TransitionDelegate transitionDelegate: const DefaultTransitionDelegate(),
	List<NavigatorObserver> observers: const []
})
```

# 方法、属性

|方法名|含义|
| --- | --- |  
|[canPop](https://api.flutter.dev/flutter/widgets/Navigator/canPop.html)| 导航器是否可以弹出。 |
|[pop](https://api.flutter.dev/flutter/widgets/Navigator/pop.html)| 弹出路由 |
|[popAndPushNamed](https://api.flutter.dev/flutter/widgets/Navigator/popAndPushNamed.html)| 将当前路线从导航器中弹出，并在其中推入已命名的路由位置 |
|[popUntil](https://api.flutter.dev/flutter/widgets/Navigator/popUntil.html)| 一直弹出直到指定路由 |
|[push](https://api.flutter.dev/flutter/widgets/Navigator/push.html)| 直接路由入栈 |
|[pushAndRemoveUntil](https://api.flutter.dev/flutter/widgets/Navigator/pushAndRemoveUntil.html)| 将具有给定名称的路由推入导航器，然后删除所有 |
|[pushNamed](https://api.flutter.dev/flutter/widgets/Navigator/pushNamed.html)| 按路由名字路由入栈 |
|[pushNamedAndRemoveUntil](https://api.flutter.dev/flutter/widgets/Navigator/pushNamedAndRemoveUntil.html)| 按路由名称将具有给定名称的路由推入导航器，然后删除所有 |
|[pushReplacement](https://api.flutter.dev/flutter/widgets/Navigator/pushReplacement.html)| 替换当前路由栈 |
|[pushReplacementNamed](https://api.flutter.dev/flutter/widgets/Navigator/pushReplacementNamed.html)|按路由名字替换当前路由栈|
|[defaultGenerateInitialRoutes](https://api.flutter.dev/flutter/widgets/Navigator/defaultGenerateInitialRoutes.html)||
|[maybePop](https://api.flutter.dev/flutter/widgets/Navigator/maybePop.html)| 导航器是否可以弹出，可以的话弹出 |
|[of](https://api.flutter.dev/flutter/widgets/Navigator/of.html)||
|[removeRoute](https://api.flutter.dev/flutter/widgets/Navigator/removeRoute.html)| 删除指定路由 |
|[removeRouteBelow](https://api.flutter.dev/flutter/widgets/Navigator/removeRouteBelow.html)| 立即从导航器中删除一条路由，然后[Route.dispose]的要替换的路线是给定的“ anchorRoute”下方的路线。 |
|[replace](https://api.flutter.dev/flutter/widgets/Navigator/replace.html)| 用新路由替换导航器上的路由 |
|[replaceRouteBelow](https://api.flutter.dev/flutter/widgets/Navigator/replaceRouteBelow.html)| 用新路由替换导航器上的路由。 路由是替换为给定anchorRoute下面的那个 |

`Navigator.push()`方式的使用：

# 使用

## 不定义路由直接跳转到新的Route

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (_) {
      return Scaffold(
        appBar: AppBar(title: Text("Demo")),
        body: FlatButton(
            onPressed: () {
              Navigator.pop(context);
            },
            child: Text("POP")),
      );
    },
  ),
);
```

<img src="/assets/images/widgets/39.gif"/>


# 资料

* [flutter.dev-Navigator Class](https://api.flutter.dev/flutter/widgets/Navigator-class.html)
* [Navigator operation requested with a context that does not include a Navigator
](https://stackoverflow.com/questions/44004451/navigator-operation-requested-with-a-context-that-does-not-include-a-navigator)