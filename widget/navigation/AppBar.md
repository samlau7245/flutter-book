
* [AppBar Class](https://api.flutter.dev/flutter/material/AppBar-class.html)
* [AppBar Design](https://material.io/components/app-bars-top)

# 构造函数

```dart
AppBar({
  Key key, // 
  Widget leading, // 在标题前显示的一个组件，在首页通常显示为应用的logo，在其他页面通常显示为返回按钮
  bool automaticallyImplyLeading: true, // 
  Widget title, // 标题
  List<Widget> actions, // 一个`Widget`列表。代表Toolbar中所展示的菜单。对于常用的菜单，通常使用`IconButton`来表示，对于不常用的菜单使用`PopupMenuButton`来显示为三个点，点击后弹出二级菜单
  Widget flexibleSpace, // 一个显示在`AppBar`下方的组件，高度和`AppBar`高度一样，可以实现一些特殊效果，通常在`SliverAppBar`中使用
  PreferredSizeWidget bottom, // 通常是`TabBar`。用来在ToolBar标题下展示菜单
  double elevation, // z坐标顺序，对于可滚动的`SliverAppBar`，当`SliverAppBar`和内容同级的时候，改值为0，当内容滚动`SliverAppBar`变为`ToolBar`的时候，修改elevation的值
  ShapeBorder shape, // 
  Color backgroundColor, // 背景色
  Brightness brightness, // `AppBar`的亮度，有白色、黑色两种主题
  IconThemeData iconTheme, // `AppBar`上图标的颜色、透明度、尺寸信息
  IconThemeData actionsIconTheme, // 
  TextTheme textTheme, // `AppBar`上文字样式
  bool primary: true, // 
  bool centerTitle, // 标题是否居中显示
  bool excludeHeaderSemantics: false, // 
  double titleSpacing: NavigationToolbar.kMiddleSpacing, // 
  double toolbarOpacity: 1.0, // 
  double bottomOpacity: 1.0 // 
)}
```

应用按钮组件有`AppBar`、`SliverAppBar`，都是继承子`StatefulWidget`类。区别在于`AppBar`固定在顶部，`SliverAppBar`可以跟着内容进行滚动。

<img src="/assets/images/flutter/14.png"/>

|SliverAppBar属性|默认值|类型|
| --- | --- | --- |
|leading|| Widget |
|automaticallyImplyLeading| true | bool |
|title|| Widget |
|actions|| List<Widget>|
|flexibleSpace|| Widget |
|bottom|| PreferredSizeWidget |
|elevation|| double |
|forceElevated| false | bool |
|backgroundColor|| Color |
|brightness|| Brightness |
|iconTheme|| IconThemeData |
|actionsIconTheme|| IconThemeData |
|textTheme|| TextTheme |
|primary| true | bool |
|centerTitle|| bool |
|excludeHeaderSemantics| false | bool |
|titleSpacing| NavigationToolbar.kMiddleSpacing | double |
|expandedHeight|| double |
|floating| false | bool |
|pinned| false | bool |
|snap| false | bool |
|stretch| false | bool |
|stretchTriggerOffset| 100.0 | double |
|onStretchTrigger|| AsyncCallback |
|shape|| ShapeBorder |

[AppBar、SliverAppBar 代码示例](https://codepen.io/samlau7245/pen/jObvOGY)

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
      home: FirstPage(),
      routes: {
        "/first": (_) => FirstPage(),
        "/second": (_) => SecondPage(),
      },
    );
  }
}

////////////////////////////////////////////////////////////////////////

class FirstPage extends StatefulWidget {
  FirstPage({Key key}) : super(key: key);

  @override
  _FirstPage createState() => new _FirstPage();
}

class _FirstPage extends State<FirstPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("First Page"),
        leading: Icon(Icons.ac_unit),
        actions: <Widget>[
          IconButton(icon: Icon(Icons.add), onPressed: null),
          IconButton(icon: Icon(Icons.search), onPressed: null)
        ],
        centerTitle: true,
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          Navigator.pushNamed(context, '/second');
        },
        child: Text('Push'),
        backgroundColor: Theme.of(context).primaryColor,
      ),
    );
  }
}

////////////////////////////////////////////////////////////////////////

class SecondPage extends StatefulWidget {
  SecondPage({Key key}) : super(key: key);
  @override
  _SecondPage createState() => new _SecondPage();
}

class _SecondPage extends State<SecondPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: CustomScrollView(
        slivers: <Widget>[
          const SliverAppBar(
            pinned: true,
            expandedHeight: 200.0,
            flexibleSpace: FlexibleSpaceBar(
              title: Text('SliverAppBar Demo'),
            ),
          ),
          SliverFixedExtentList(
            itemExtent: 50.0,
            delegate: SliverChildBuilderDelegate(
              (BuildContext context, int index) {
                return Container(
                  alignment: Alignment.center,
                  color: Colors.lightBlue[100 * (index % 9)],
                  child: Text('List Item $index'),
                );
              },
            ),
          ),
        ],
      ),
    );
  }
}
```

# 资料

* [SliverAppBar(应用按钮组件)](https://api.flutter.dev/flutter/material/SliverAppBar-class.html)