
# [MaterialApp(应用组件)](https://api.flutter.dev/flutter/material/MaterialApp-class.html)

# 构造函数

```dart
const MaterialApp({
  Key key,
  GlobalKey<NavigatorState> navigatorKey,
  Widget home,
  Map<String, WidgetBuilder> routes: const {},
  String initialRoute,
  RouteFactory onGenerateRoute,
  InitialRouteListFactory onGenerateInitialRoutes,
  RouteFactory onUnknownRoute,
  List<NavigatorObserver> navigatorObservers: const [],
  TransitionBuilder builder,
  String title: '',
  GenerateAppTitle onGenerateTitle,
  Color color,
  ThemeData theme,
  ThemeData darkTheme,
  ThemeMode themeMode: ThemeMode.system,
  Locale locale,
  Iterable<LocalizationsDelegate> localizationsDelegates,
  LocaleListResolutionCallback localeListResolutionCallback,
  LocaleResolutionCallback localeResolutionCallback,
  Iterable<Locale> supportedLocales: const [Locale('en', 'US')],
  bool debugShowMaterialGrid: false,
  bool showPerformanceOverlay: false,
  bool checkerboardRasterCacheImages: false,
  bool checkerboardOffscreenLayers: false,
  bool showSemanticsDebugger: false,
  bool debugShowCheckedModeBanner: true, // 隐藏Debug标签
  Map<LogicalKeySet, Intent> shortcuts,
  Map<Type, Action<Intent>> actions
})
```

|属性|类型|说明|
| --- | --- | --- |
|title|String|应用程序的标题：<br>iOS->程序切换管理器中<br>Android->任务管理器的程序快照上|
|theme|[ThemeData](https://api.flutter.dev/flutter/material/ThemeData-class.html)|应用使用的主题色，可以全局也可以局部设置|
|color|[Color](https://api.flutter.dev/flutter/dart-ui/Color-class.html)|应用的主题色：`primary color`|
|home|Widget|用来定义当前应用打开时,所显示的界面|
|routes|Map<String,WidgetBuilder>|应用中页面跳转规则|
|initialRoute|String|初始化路由|
|onGenerateRoute|[RouteFactory](https://api.flutter.dev/flutter/widgets/RouteFactory.html)|路由回调函数。当通过`Navigator.of(context).pushNamed`跳转路由时，在`routes`查找不到时，会调用该方法|
|onLocalChanged||当系统修改语言的时候,会触发这个回调|
|navigatorObservers|`List<NavigatorObserver>`|导航观察器|
|debugShowMaterialGrid|bool|是否显示纸墨设计基础布局网格,用来调试UI的工具|
|showPerformanceOverlay|bool|显示性能标签|

`MaterialApp`中`Navigator`寻找页面的顺序:

* For the `/` route, the `home` property, if non-null, is used.
* Otherwise, the `routes` table is used, if it has an entry for the route.
* Otherwise, `onGenerateRoute` is called, if provided. It should return a non-null value for any valid route not handled by home and routes.
* Finally if all else fails `onUnknownRoute` is called.

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "MaterialApp Demo",
      theme: ThemeData(primaryColor: Colors.blue),
      color: Colors.orange,
      home: HomePage(),
      routes: {
        "/first": (_) => FirstPage(),
        "/second": (_) => SecondPage(),
        "/thirs": (_) => ThirdPage(),
      },
    );
  }
}

// 等效于：

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "MaterialApp Demo",
      theme: ThemeData(primaryColor: Colors.blue),
      color: Colors.orange,
      routes: {
        "/": (_) => HomePage(),
        "/first": (_) => FirstPage(),
        "/second": (_) => SecondPage(),
        "/thirs": (_) => ThirdPage(),
      },
      initialRoute: '/',
    );
  }
}
```

下面是示例，具体效果查看[CodePen](https://codepen.io/samlau7245/pen/jObpgKo)

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "MaterialApp Demo",
      theme: ThemeData(primaryColor: Colors.blue),
      color: Colors.orange,
      home: HomePage(),
      routes: {
        "/first": (_) => FirstPage(),
        "/second": (_) => SecondPage(),
        "/thirs": (_) => ThirdPage(),
      },
      onGenerateRoute: (RouteSettings settings) {
        // 路由回调函数。当通过`Navigator.of(context).pushNamed`跳转路由时，在`routes`查找不到时，会调用该方法
        print(settings.name + settings.arguments);
        return null;
      },
    );
  }
}

////////////////////////////////////////////////////////////////////////

class HomePage extends StatefulWidget {
  @override
  _HomePage createState() => new _HomePage();
}

class _HomePage extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Home Page"),
      ),
      body: Center(child: Text('Home')),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          Navigator.pushNamed(context, '/first');
        },
        child: Text('Push'),
      ),
    );
  }
}

////////////////////////////////////////////////////////////////////////

class FirstPage extends StatefulWidget {
  @override
  _FirstPage createState() => new _FirstPage();
}

class _FirstPage extends State<FirstPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("First Page"),
      ),
      body: Center(child: Text('First')),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          if (Navigator.canPop(context)) {
            Navigator.popAndPushNamed(context, '/second');
          }
        },
        child: Text('Pop'),
      ),
    );
  }
}

////////////////////////////////////////////////////////////////////////

class SecondPage extends StatefulWidget {
  @override
  _SecondPage createState() => new _SecondPage();
}

class _SecondPage extends State<SecondPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Second Page"),
      ),
      body: Center(child: Text('Second')),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          Navigator.push(context, MaterialPageRoute<void>(builder: (_) {
            return Scaffold(
              appBar: AppBar(
                title: Text('MaterialPageRoute Demo'),
              ),
              body: Center(
                child: Text("MaterialPageRoute Demo"),
              ),
            );
          }));
        },
        child: Text('Push'),
      ),
    );
  }
}

////////////////////////////////////////////////////////////////////////

class ThirdPage extends StatefulWidget {
  @override
  _ThirdPage createState() => new _ThirdPage();
}

class _ThirdPage extends State<ThirdPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Third Page"),
      ),
      body: Center(child: Text('Third')),
    );
  }
}
```