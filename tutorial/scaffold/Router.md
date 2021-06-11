# 使用 onGenerateRoute 实现

```dart
return MaterialApp(
  onGenerateRoute: (RouteSettings settings) {
    switch (settings.name) {
      case '/':
        return MaterialPageRoute(builder: (_) => App());
      case '/login':
        return MaterialPageRoute(builder: (_) => LoginPage());
      default:
        return MaterialPageRoute(builder: (_) => Error404Page());
    }
  },
  // home: App(),
);
```