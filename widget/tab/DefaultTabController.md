
[DefaultTabController Class](https://api.flutter.dev/flutter/material/DefaultTabController-class.html)

# 构造函数

```dart
const DefaultTabController({
	Key key,
	@required int length,
	int initialIndex: 0,
	@required Widget child
})
```

# 示例

```dart
class _AppBarExample01State extends State<AppBarExample01>
    with SingleTickerProviderStateMixin {
  TabController _tabController;
  List tabs = [];

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
    return DefaultTabController(
        length: tabs.length,
        child: MaterialApp(
          home: Scaffold(
            appBar: AppBar(
              title: TabBar(
                tabs: tabs,
                controller: _tabController,
                isScrollable: true,
                indicatorColor: Color(0xffff0000),
                indicatorWeight: 1,
                indicatorSize: TabBarIndicatorSize.tab,
                indicatorPadding: EdgeInsets.only(bottom: 10.0),
                labelPadding: EdgeInsets.only(left: 20),
                labelColor: Color(0xff333333),
                labelStyle: TextStyle(
                  fontSize: 15.0,
                ),
                unselectedLabelColor: Color(0xffffffff),
                unselectedLabelStyle: TextStyle(
                  fontSize: 12.0,
                ),
              ),
            ),
            body: TabBarView(
              controller: _tabController,
              children: tabs.map((e) => Container()).toList(),
            ),
          ),
        ));
  }

  @override
  void dispose() {
    _tabController.dispose();
    super.dispose();
  }
}
```

<img src="/assets/images/widgets/15.png"/>