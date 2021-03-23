
# BottomAppBar

```dart
void main() {
  runApp(BottomBarApp());
}

class BottomBarApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'BottomBarApp',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('BottomBarApp Home Page'),
      ),
      bottomNavigationBar: BottomAppBar(
        child: Row(
          mainAxisAlignment: MainAxisAlignment.spaceAround,
          children: [
            IconButton(icon: Icon(Icons.home), onPressed: () {}),
            IconButton(icon: Icon(Icons.shop), onPressed: () {}),
            IconButton(icon: Icon(Icons.message), onPressed: () {}),
            IconButton(icon: Icon(Icons.people), onPressed: () {}),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {},
        child: Icon(Icons.post_add),
      ),
      floatingActionButtonLocation: FloatingActionButtonLocation.centerDocked,
    );
  }
}
```

<img src="/assets/images/bottomBar/01.png"/>

其中还有一些扩展效果的属性:

```dart
BottomAppBar(
  shape: CircularNotchedRectangle(),
  elevation: 8.0,
  notchMargin: 10,
  //...
)
//...
```

* `shape`: 表示`FloatingActionButton`嵌入到`BottomAppBar`中。
* `elevation`: 阴影。
* `notchMargin`: 表示缺口外边距。

<img src="/assets/images/bottomBar/02.png"/>

# BottomNavigationBar、BottomNavigationBarItem

[BottomNavigationBar](https://api.flutter.dev/flutter/material/BottomNavigationBar-class.html)和[BottomNavigationBarItem](https://api.flutter.dev/flutter/widgets/BottomNavigationBarItem-class.html)配合`Scaffold`组件可以实现底部导航栏效果。

```dart
BottomNavigationBar({Key? key, 
    required List<BottomNavigationBarItem> items, 
    
    ValueChanged<int>? onTap, 
    int currentIndex: 0, 
    BottomNavigationBarType? type, // 默认：shifting
    MouseCursor? mouseCursor
    
    Color? fixedColor, 
    Color? backgroundColor, 
    double iconSize: 24.0, 
    double? elevation, 

    Color? selectedItemColor, 
    Color? unselectedItemColor, 

    double selectedFontSize: 14.0, 
    double unselectedFontSize: 12.0, 
    
    IconThemeData? selectedIconTheme, 
    IconThemeData? unselectedIconTheme, 
   
    TextStyle? selectedLabelStyle, 
    TextStyle? unselectedLabelStyle, 
   
    bool? showSelectedLabels, 
    bool? showUnselectedLabels, 
})

enum BottomNavigationBarType {
  fixed, // Bottom Navigation 固定位置，They don’t scroll or move horizontally.
  shifting, // animate and labels fade in when they are tapped.
}
```

```dart
BottomNavigationBarItem({
    required Widget icon, 
    
    Widget? title, // @Deprecated: 使用 label 代替。
    String? label, 

    Widget? activeIcon, 
    Color? backgroundColor, 
    String? tooltip
})
```

示例代码：

```dart
class MyHomePage2 extends StatefulWidget {
  @override
  _MyHomePage2State createState() => _MyHomePage2State();
}

class _MyHomePage2State extends State<MyHomePage2> {
  var items = <BottomNavigationBarItem>[
    BottomNavigationBarItem(icon: Icon(Icons.home), label: '首页'),
    BottomNavigationBarItem(icon: Icon(Icons.shop), label: '商城'),
    BottomNavigationBarItem(icon: Icon(Icons.message), label: '消息'),
    BottomNavigationBarItem(icon: Icon(Icons.people), label: '我的'),
  ];

  int _selectedIndex = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('BottomNavigationBar Demo')),
      bottomNavigationBar: BottomNavigationBar(
        items: items,
        type: BottomNavigationBarType.fixed,
        selectedItemColor: Theme.of(context).primaryColor,
        unselectedItemColor: Theme.of(context).unselectedWidgetColor,
        currentIndex: _selectedIndex,
        onTap: (index) {
          setState(() {
            _selectedIndex = index;
          });
        },
      ),
    );
  }
}
```

<img src="/assets/images/bottomBar/03.gif"/>

# 其他

* [Flutter Favorite: bottom_navy_bar](https://pub.dev/packages/bottom_navy_bar)





















