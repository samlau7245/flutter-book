
[TabBar Class](https://api.flutter.dev/flutter/material/TabBar-class.html)

# 构造函数

```dart
const TabBar({
  Key key,
  @required List<Widget> tabs, // Tab选项列表，建议不要放太多项，否则用户操作起来不方便
  TabController controller, // 如果 TabController 没有提供，那默认会使用 DefaultTabController
  bool isScrollable: false, // 是否可以水平移动
  Color indicatorColor,//指示器颜色
  double indicatorWeight: 2.0,//指示器高度
  EdgeInsetsGeometry indicatorPadding: EdgeInsets.zero,//底部指示器的Padding
  Decoration indicator,//指示器decoration，例如边框等
  TabBarIndicatorSize indicatorSize,//指示器大小计算方式
  Color labelColor,//选中label颜色
  TextStyle labelStyle,//选中label的Style
  EdgeInsetsGeometry labelPadding,//每个label的padding值
  Color unselectedLabelColor,//未选中label颜色
  TextStyle unselectedLabelStyle,//未选中label的Style
  DragStartBehavior dragStartBehavior: DragStartBehavior.start,
  ValueChanged<int> onTap
})
```

# 示例

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  // 选项卡 数据源
  final List<Tab> tabs = [
    Tab(text: '选项卡 1',),
    Tab(text: '选项卡 2',),
    Tab(text: '选项卡 3',),
  ];

  // 应用程序的主组件
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      home: DefaultTabController(
        child: new Scaffold(
          appBar: new AppBar(
            // 添加导航栏
            bottom: TabBar(tabs: tabs),
          ),
          body: TabBarView(children: tabs.map((Tab tab){
            return Center(
              child: Text(tab.text),
            );
          }).toList()),
        ), 
        length: tabs.length,),
    );
  }
}
```

<img src="/assets/images/flutter/17.png" width = "25%" height = "25%"/>

实现一个完整示例：

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      // DefaultTabController：关联 TabBar 和 TabBarView
      home: DefaultTabController(
        child: new Scaffold(
          appBar: new AppBar(
            bottom: TabBar(
              // 设置可滚动
              isScrollable: true,
              tabs: items.map((ItemView item) {
                return Tab(
                  text: item.title,
                  icon: new Icon(item.icon),
                );
              }).toList(),
            ),
          ),
          body: new TabBarView(
              children: items.map((ItemView item) {
            return new Padding(
              padding: const EdgeInsets.all(16.0),
              child: new SelectedView(item: item),
            );
          }).toList()),
        ),
        length: items.length,
      ),
    );
  }
}

// 选项卡数据结构
class ItemView {
  // 构造函数
  const ItemView({this.title, this.icon});
  final String title;
  final IconData icon;
}

// 选项卡数据源
const List<ItemView> items = [
  const ItemView(title: '自驾', icon: Icons.directions_car),
  const ItemView(title: '自行车', icon: Icons.directions_bike),
  const ItemView(title: '轮船', icon: Icons.directions_boat),
  const ItemView(title: '公交车', icon: Icons.directions_bus),
  const ItemView(title: '火车', icon: Icons.directions_railway),
  const ItemView(title: '步行', icon: Icons.directions_walk),
];

// 被选中的视图->被装载在 TabBarView 里面
class SelectedView extends StatelessWidget {
  const SelectedView({Key key, this.item}) : super(key: key);
  final ItemView item;

  @override
  Widget build(BuildContext context) {
    final TextStyle textStyle = Theme.of(context).textTheme.display1;

    return new Card(
      color: Colors.white,
      child: new Center(
        child: new Column(
          mainAxisSize: MainAxisSize.min, // 垂直方向最小化处理
          crossAxisAlignment: CrossAxisAlignment.center, //水平方向居中对齐
          children: <Widget>[
            new Icon(
              item.icon,
              size: 128.0,
              color: textStyle.color,
            ),
            new Text(
              item.title,
              style: textStyle,
            )
          ],
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/18.png" width = "25%" height = "25%"/>

### 示例2

```dart
class _AppBarExample01State extends State<AppBarExample02>
    with SingleTickerProviderStateMixin {
  TabController _tabController;
  List<Tab> tabs = [];

  @override
  void initState() {
    tabs = <Tab>[
      Tab(text: "Tab1"),
      Tab(text: "Tab2"),
      Tab(text: "Tab3"),
      Tab(text: "Tab4"),
      Tab(text: "Tab5"),
      Tab(text: "Tab6"),
      Tab(text: "Tab7"),
      Tab(text: "Tab8"),
      Tab(
        text: "Tab9",
        icon: Icon(Icons.phone),
      )
    ];

    _tabController =
        TabController(initialIndex: 2, length: tabs.length, vsync: this);
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("AppBarExample02"),
        bottom: TabBar(
          tabs: tabs,
          controller: _tabController,
          isScrollable: true,
        ),
      ),
      body: TabBarView(
        children: tabs
            .map((Tab tab) => Container(
                  child: Center(
                    child: Text(tab.text),
                  ),
                ))
            .toList(),
        controller: _tabController,
      ),
    );
  }

  @override
  void dispose() {
    _tabController.dispose();
    super.dispose();
  }
}
```

<img src="/assets/images/widgets/16.png"/>