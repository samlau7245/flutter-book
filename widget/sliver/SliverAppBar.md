
[SliverAppBar Class](https://api.flutter.dev/flutter/material/SliverAppBar-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/R9C5KMJKluE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
const SliverAppBar({
	Key key,
	Widget leading, 左侧控件，通常情况下为"返回"图标
	Widget title, 标题，通常为Text控件
	List<Widget> actions, 右侧控件
	PreferredSizeWidget bottom, 底部控件

	bool forceElevated: false, //是否显示阴影
	double elevation, 阴影

	double titleSpacing: NavigationToolbar.kMiddleSpacing, //标题横向间距
	double stretchTriggerOffset: 100.0,

	bool automaticallyImplyLeading: true, //没有leading为true的时候，默认返回箭头
	bool primary: true, //是否显示在状态栏的下面,false就会占领状态栏的高度
	bool centerTitle, 标题是否在中间
	bool excludeHeaderSemantics: false,

	Color backgroundColor, 背景颜色
	Brightness brightness, //状态栏主题，默认Brightness.dark，可选参数light
	AsyncCallback onStretchTrigger,
	ShapeBorder shape,

	IconThemeData iconTheme,
	IconThemeData actionsIconTheme,
	TextTheme textTheme,
    
	Widget flexibleSpace, 是SliverAppBar中展开和折叠区域
	double expandedHeight, 是表示flexibleSpace的高度

	bool floating: false, 设置为true时，向下滑动时，即使当前CustomScrollView不在顶部，SliverAppBar也会跟着一起向下出现
	bool snap: false, 设置为true时，当手指放开时，SliverAppBar会根据当前的位置进行调整，始终保持展开或收起的状态，此效果在floating=true时生效
	bool pinned: false, 设置为true时，当SliverAppBar内容滑出屏幕时，将始终渲染一个固定在顶部的收起状态

	bool stretch: false,
})
```

`SliverAppBar` 控件需要和`CustomScrollView`搭配使用，`SliverAppBar`要通常放在`slivers`的第一位，后面接其他`slive`控件。

## pinned 属性控制

当`pinned=false`的时候：

<img src="/assets/images/widgets/47.gif"/>

当`pinned=true`的时候：

<img src="/assets/images/widgets/48.gif"/>

具体的代码：

```daart
@override
Widget build(BuildContext context) {
  return CustomScrollView(
    slivers: [
      SliverAppBar(
        leading: IconButton(
          icon: Icon(Icons.arrow_back),
          onPressed: () {},
        ),
        title: Text("SliverAppBar"),
        actions: [
          IconButton(
            icon: Icon(Icons.home),
            onPressed: () {},
          ),
          IconButton(
            icon: Icon(Icons.exit_to_app),
            onPressed: () {},
          ),
        ],
        actionsIconTheme: IconThemeData(color: Colors.blue),
        backgroundColor: Colors.red[100],
        centerTitle: true,
        pinned: true,
        expandedHeight: 150,
      ),
      SliverGrid(
        delegate: SliverChildBuilderDelegate(
          (_, index) {
            return Container(
              color: Colors.primaries[index % Colors.primaries.length],
            );
          },
          childCount: 20,
        ),
        gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: 2,
          mainAxisSpacing: 5,
          crossAxisSpacing: 5,
        ),
      ),
    ],
  );
}
```

## 展示阴影

```dart
SliverAppBar(
  elevation: 10.0,
  forceElevated: true,
  ...
),
```

下面就是展示阴影和不展示阴影的区别：

<img src="/assets/images/widgets/49.png"/>

## 添加滑动标题


```dart
@override
Widget build(BuildContext context) {
  return CustomScrollView(
    slivers: [
      SliverAppBar(
        //title: Text("SliverAppBar"),
        leading: IconButton(
          icon: Icon(Icons.arrow_back),
          onPressed: () {},
        ),
        pinned: true,
        expandedHeight: 150,
        flexibleSpace: FlexibleSpaceBar(
          title: Text("SliverAppBar"),
          collapseMode: CollapseMode.pin,
        ),
      ),
      SliverGrid(
        delegate: SliverChildBuilderDelegate(
          (_, index) {
            return Container(
              color: Colors.primaries[index % Colors.primaries.length],
            );
          },
          childCount: 20,
        ),
        gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: 2,
          mainAxisSpacing: 5,
          crossAxisSpacing: 5,
        ),
      ),
    ],
  );
}
```

<img src="/assets/images/widgets/50.gif"/>

## 添加背景图

```dart
@override
Widget build(BuildContext context) {
  return CustomScrollView(
    slivers: [
      SliverAppBar(
        flexibleSpace: FlexibleSpaceBar(
          background: Image.asset(Constant.ASSETS_IMG + 'hot_search_top.png'),
        ),
        ...
      ),
      ...
    ],
  );
}
```

<img src="/assets/images/widgets/51.gif"/>