
[Scaffold Class](https://api.flutter.dev/flutter/material/Scaffold-class.html)

# 构造函数

```dart
const Scaffold({
  Key key,
  PreferredSizeWidget appBar, // 显示在界面顶部的一个AppBar
  Widget body, // 当前界面所显示的主要内容
  
  Widget floatingActionButton, // Material Design中定义的一个功能按钮
  FloatingActionButtonLocation floatingActionButtonLocation,
  FloatingActionButtonAnimator floatingActionButtonAnimator,
  
  List<Widget> persistentFooterButtons, // 固定在下方显示的按钮
  Widget drawer, // 侧边栏组件
  Widget endDrawer,
  Widget bottomNavigationBar, // 显示在底部的导航栏按钮栏
  Widget bottomSheet,
  Color backgroundColor, // 背景颜色
  bool resizeToAvoidBottomPadding, // 控制界面内容`body`是否重新布局来避免底部被覆盖,比如当键盘显示时,重新布局避免被键盘盖住内容。默认值为`true`
  bool resizeToAvoidBottomInset,
  bool primary: true,
  DragStartBehavior drawerDragStartBehavior: DragStartBehavior.start,
  bool extendBody: false,
  bool extendBodyBehindAppBar: false,
  Color drawerScrimColor,
  double drawerEdgeDragWidth,
  bool drawerEnableOpenDragGesture: true,
  bool endDrawerEnableOpenDragGesture: true
})
```

示例代码：[codePen](https://codepen.io/samlau7245/pen/XWmPrZe)

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "MaterialApp Demo",
      theme: ThemeData(primaryColor: Color(0xFF37966F)),
      color: Colors.orange,
      home: HomePage(),
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
      // 头部元素
      appBar: AppBar(title: Text("Home Page")),
      // 视图部份
      body: Center(child: Text('Home')),
      // 抽屉
      drawer: Drawer(),
      bottomNavigationBar: BottomAppBar(
        shape: const CircularNotchedRectangle(),
        color: Color(0xFF37966F),
        child: Container(
          height: 50.0,
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {},
        backgroundColor: Color(0xFF37966F),
        child: Icon(Icons.add),
      ),
      floatingActionButtonLocation: FloatingActionButtonLocation.centerDocked,
    );
  }
}
```

* [关于`Scaffold.of() called with a context that does not contain a Scaffold.`的报错解决方案](https://stackoverflow.com/questions/51304568/scaffold-of-called-with-a-context-that-does-not-contain-a-scaffold)
