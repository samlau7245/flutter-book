
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
