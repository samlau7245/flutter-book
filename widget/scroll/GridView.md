
[GridView Class](https://api.flutter.dev/flutter/widgets/GridView-class.html)

# 构造函数

```dart
GridView({
	Key key, 
  Axis scrollDirection: Axis.vertical, 
  bool reverse: false, 
  ScrollController controller, 
  bool primary, 
  ScrollPhysics physics, 
  bool shrinkWrap: false, 
  EdgeInsetsGeometry padding, 
  @required SliverGridDelegate gridDelegate, // 布局代理
  bool addAutomaticKeepAlives: true, 
  bool addRepaintBoundaries: true, 
  bool addSemanticIndexes: true, 
  double cacheExtent, 
  List<Widget> children: const [], 
  int semanticChildCount, 
  DragStartBehavior dragStartBehavior: DragStartBehavior.start, 
  ScrollViewKeyboardDismissBehavior keyboardDismissBehavior: ScrollViewKeyboardDismissBehavior.manual
})

GridView.builder({
	Key key, 
  Axis scrollDirection: Axis.vertical, 
  bool reverse: false, 
  ScrollController controller, 
  bool primary, 
  ScrollPhysics physics, 
  bool shrinkWrap: false, 
  EdgeInsetsGeometry padding, 
  @required SliverGridDelegate gridDelegate, 
  @required IndexedWidgetBuilder itemBuilder, 
  int itemCount, 
  bool addAutomaticKeepAlives: true, 
  bool addRepaintBoundaries: true, 
  bool addSemanticIndexes: true, 
  double cacheExtent, 
  int semanticChildCount, 
  DragStartBehavior dragStartBehavior: DragStartBehavior.start, 
  ScrollViewKeyboardDismissBehavior keyboardDismissBehavior: ScrollViewKeyboardDismissBehavior.manual
})

GridView.count({
	Key key, 
  Axis scrollDirection: Axis.vertical, 
  bool reverse: false, 
  ScrollController controller, 
  bool primary, 
  ScrollPhysics physics, 
  bool shrinkWrap: false, 
  EdgeInsetsGeometry padding, 
  @required int crossAxisCount, 
  double mainAxisSpacing: 0.0, 
  double crossAxisSpacing: 0.0, 
  double childAspectRatio: 1.0, 
  bool addAutomaticKeepAlives: true, 
  bool addRepaintBoundaries: true, 
  bool addSemanticIndexes: true, 
  double cacheExtent, 
  List<Widget> children: const [], 
  int semanticChildCount, 
  DragStartBehavior dragStartBehavior: DragStartBehavior.start, 
  ScrollViewKeyboardDismissBehavior keyboardDismissBehavior: ScrollViewKeyboardDismissBehavior.manual
})

GridView.custom({
	Key key, 
  Axis scrollDirection: Axis.vertical, 
  bool reverse: false, 
  ScrollController controller, 
  bool primary, 
  ScrollPhysics physics, 
  bool shrinkWrap: false, 
  EdgeInsetsGeometry padding, 
  @required SliverGridDelegate gridDelegate, 
  @required SliverChildDelegate childrenDelegate, 
  double cacheExtent, 
  int semanticChildCount, 
  DragStartBehavior dragStartBehavior: DragStartBehavior.start, 
  ScrollViewKeyboardDismissBehavior keyboardDismissBehavior: ScrollViewKeyboardDismissBehavior.manual
})

GridView.extent({
	Key key, 
  Axis scrollDirection: Axis.vertical, 
  bool reverse: false, 
  ScrollController controller, 
  bool primary, 
  ScrollPhysics physics, 
  bool shrinkWrap: false, 
  EdgeInsetsGeometry padding, 
  @required double maxCrossAxisExtent, 
  double mainAxisSpacing: 0.0, 
  double crossAxisSpacing: 0.0, 
  double childAspectRatio: 1.0, 
  bool addAutomaticKeepAlives: true, 
  bool addRepaintBoundaries: true, 
  bool addSemanticIndexes: true, 
  List<Widget> children: const [], 
  int semanticChildCount, 
  DragStartBehavior dragStartBehavior: DragStartBehavior.start, 
  ScrollViewKeyboardDismissBehavior keyboardDismissBehavior: ScrollViewKeyboardDismissBehavior.manual
})

```

# 示例

```dart
Widget gridViewItem(GridItemModel itemModel) {
    return Column(
      children: [
        Image.asset(itemModel.pic),
        Text(itemModel.name),
      ],
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('GridviewExample'),
      ),
      body: GridView.count(
        crossAxisCount: 5,
        children: list.map((GridItemModel e) {
          return gridViewItem(e);
        }).toList(),
      ),
    );
  }
}
```

<img src="/assets/images/widgets/36.png"/>

```dart
flutter: The overflowing RenderFlex has an orientation of Axis.vertical.
flutter: The edge of the RenderFlex that is overflowing has been marked in the rendering with a yellow and
flutter: black striped pattern. This is usually caused by the contents being too big for the RenderFlex.
flutter: Consider applying a flex factor (e.g. using an Expanded widget) to force the children of the
flutter: RenderFlex to fit within the available space instead of being sized to their natural size.
flutter: This is considered an error condition because it indicates that there is content that cannot be
flutter: seen. If the content is legitimately bigger than the available space, consider clipping it with a
flutter: ClipRect widget before putting it in the flex, or using a scrollable container rather than a Flex,
flutter: like a ListView.
flutter: The specific RenderFlex in question is: RenderFlex#7b07d OVERFLOWING:
flutter:   creator: Column ← RepaintBoundary ← IndexedSemantics ← NotificationListener<KeepAliveNotification> ←
flutter:     KeepAlive ← AutomaticKeepAlive ← KeyedSubtree ← SliverGrid ← MediaQuery ← SliverPadding ← Viewport
flutter:     ← IgnorePointer-[GlobalKey#b6ba6] ← ⋯
flutter:   parentData: <none> (can use size)
flutter:   constraints: BoxConstraints(w=75.0, h=75.0)
flutter:   size: Size(75.0, 75.0)
flutter:   direction: vertical
flutter:   mainAxisAlignment: start
flutter:   mainAxisSize: max
flutter:   crossAxisAlignment: center
flutter:   verticalDirection: down
flutter: ◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤◢◤
flutter: ════════════════════════════════════════════════════════════════════════════════════════════════════
flutter: Another exception was thrown: A RenderFlex overflowed by 2.0 pixels on the bottom.
flutter: Another exception was thrown: A RenderFlex overflowed by 19 pixels on the bottom.
flutter: Another exception was thrown: A RenderFlex overflowed by 19 pixels on the bottom.
flutter: Another exception was thrown: A RenderFlex overflowed by 19 pixels on the bottom.
flutter: Another exception was thrown: A RenderFlex overflowed by 2.0 pixels on the bottom.
flutter: Another exception was thrown: A RenderFlex overflowed by 19 pixels on the bottom.
```

可以看到布局报错，`GridView`中`child`内的布局超过了规定约束的大小。

# GridView(网格列表布局)

网格列表组件(GridView)：克实现多行多列的应用场景。

* `GridView.count`： 允许你制定列的数量。
* `GridView.extent`： 允许你制定单元格的最大宽度。

| 属性 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
|scrollDirection|||
|reverse|||
|controller|||
|primary|bool||是否是与父节点的PrimaryScrollController所关联的主滚动视图|
|physics|||
|shrinkWrap|||
|padding|||
|gridDelegate|SliverGridDelegate||控制GridView中节点布局的delegate|
|cacheExtent|||

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    List<Widget> widgets = new List<Widget>.generate(20, (i) => new Text('data'));
    return MaterialApp(
      home: new Scaffold(
        appBar: new AppBar(
          title: new Text('Bar title'),
        ),
        body: new GridView.count(
          crossAxisCount: 3,// 一行上放三列数据
          primary: false,
          padding: const EdgeInsets.all(20.0),
          crossAxisSpacing: 30.0,
          children: widgets,
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/08.png" width = "25%" height = "25%"/>

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    List<Container> _buildGridTitleList(int count) {
      return new List<Container>.generate(count, (int index) {
        return new Container(
          child: new Image.asset('icons/code.png',),
        );
      });
    }

    Widget buildGrid() {
      return new GridView.extent(
        maxCrossAxisExtent: 150.0, // 次轴最大宽度
        padding: const EdgeInsets.all(4.0),
        mainAxisSpacing: 4.0, // 主轴间隙
        crossAxisSpacing: 4.0, // 次轴间隙
        children: _buildGridTitleList(9),
      );
    }

    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(
          title: Text('data'),
        ),
        body: new Center(
          child: buildGrid(),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/53.png" width = "25%" height = "25%"/>