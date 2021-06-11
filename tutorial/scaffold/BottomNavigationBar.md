# BottomNavigationBar 底部导航条

* [BottomNavigationBar class](https://pub.flutter-io.cn/documentation/base/latest/flutter_material_bottom_navigation_bar/BottomNavigationBar-class.html)

# 需求

* 去除底部Item点击默认的波纹效果

```dart
Widget build(BuildContext context) {
  return MaterialApp(
    title: 'Demo',
    theme: ThemeData(
      highlightColor: Color.fromRGBO(0, 0, 0, 0), // Add
      splashColor: Color.fromRGBO(0, 0, 0, 0), // Add
    ),
    home: App(),
  );
}
```