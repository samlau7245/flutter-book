# [Scaffold(脚手架组件)](https://api.flutter.dev/flutter/material/Scaffold-class.html)

|属性|类型|说明|
| --- | --- | --- |
|appBar|AppBar|显示在界面顶部的一个AppBar|
|body|Widget|当前界面所显示的主要内容|
|floatingActionButton|Widget|Material Design中定义的一个功能按钮|
|persistentFooterButtons|List<Widget>|固定在下方显示的按钮|
|drawer|Widget|侧边栏组件|
|botlomNavigationBar|Widget|显示在底部的导航栏按钮栏|
|backgroundcolor|Color|背景颜色|
|resizeToAvoidBottomPadding| bool|控制界面内容`body`是否重新布局来避免底部被覆盖,比如当键盘显示时,重新布局避免被键盘盖住内容。默认值为`true`|

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
