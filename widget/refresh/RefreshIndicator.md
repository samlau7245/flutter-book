
[RefreshIndicator](https://api.flutter.dev/flutter/material/RefreshIndicator-class.html)

# 构造函数

```dart
const RefreshIndicator({
	Key key,
	@required Widget child,
	double displacement: 40.0,
	@required RefreshCallback onRefresh,
	Color color,
	Color backgroundColor,
	ScrollNotificationPredicate notificationPredicate: defaultScrollNotificationPredicate,
	String semanticsLabel,
	String semanticsValue,
	double strokeWidth: 2.0
})
```

# 示例

```dart
class _WeiboFindPageState extends State<WeiboFindPage> {
  int listCount = 0;
  Future<Null> loadData() async {
    print("load started!");
    await Future.delayed(Duration(seconds: 3)).then((value) {
      setState(() {
        listCount = 20;
        print("load finished!");
        return null;
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("刷新"),
      ),
      body: RefreshIndicator(
        onRefresh: loadData,
        child: ListView.builder(
          itemBuilder: (_, index) {
            return Container(
              height: 100,
              color: Colors.primaries[index % Colors.primaries.length],
              child: Center(
                child: Text("data-$index"),
              ),
            );
          },
          itemCount: listCount,
        ),
      ),
    );
  }
}
```

<img src="/assets/images/widgets/62.gif"/>


## 上拉刷新

```dart
class _WeiboFindPageState extends State<WeiboFindPage> {
  ScrollController _scrollController = ScrollController();
  int listCount = 10;

  @override
  void initState() {
    _scrollController.addListener(() {
      // 判断是否滑动到底部
      if (_scrollController.position.pixels ==
          _scrollController.position.maxScrollExtent) {
        loadData(); // 加载更多
      }
    });
    loadData(); // 初始化数据
    super.initState();
  }

  @override
  void dispose() {
    _scrollController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("刷新"),
      ),
      body: RefreshIndicator(
        onRefresh: loadData,
        child: CustomScrollView(
          slivers: [
            SliverList(
              delegate: SliverChildBuilderDelegate(
                (_, index) {
                  return Container(
                    height: 100,
                    color: Colors.primaries[index % Colors.primaries.length],
                    child: Center(
                      child: Text("$index"),
                    ),
                  );
                },
                childCount: 20,
              ),
            ),
            SliverToBoxAdapter(
              child: Container(
                height: 100,
                child: Center(
                  child: Text("加载更多"),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }

  Future<Null> loadData() async {
    print("load started!");
    await Future.delayed(Duration(seconds: 1)).then((value) {
      setState(() {
        listCount = 20;
        print("load finished!");
        return null;
      });
    });
  }
}
```

<img src="/assets/images/widgets/63.gif"/>

