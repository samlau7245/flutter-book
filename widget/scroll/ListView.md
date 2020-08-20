
[ListView Class](https://api.flutter.dev/flutter/widgets/ListView-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/KJpkjHGiI5A" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
ListView({
  Key key, 
  Axis scrollDirection: Axis.vertical, // 列表的滚动方向
  bool reverse: false, 
  ScrollController controller, // 控制器，与列表滚动相关，比如监听列表的滚动事件
  bool primary, 
  ScrollPhysics physics,  // 列表滚动至边缘后继续拖动的物理效果，Android与iOS效果不同。
  bool shrinkWrap: false, // 决定列表的长度是否仅包裹其内容的长度。当ListView嵌在一个无限长的容器组件中时，shrinkWrap必须为true，否则Flutter会给出警告
  EdgeInsetsGeometry padding, // 列表内边距
  double itemExtent, // 子元素长度。当列表中的每一项长度是固定的情况下可以指定该值，有助于提高列表的性能
  bool addAutomaticKeepAlives: true, 
  bool addRepaintBoundaries: true, 
  bool addSemanticIndexes: true, 
  double cacheExtent, // 预渲染区域长度
  List<Widget> children: const [], 
  int semanticChildCount, 
  DragStartBehavior dragStartBehavior: DragStartBehavior.start, 
  ScrollViewKeyboardDismissBehavior keyboardDismissBehavior: ScrollViewKeyboardDismissBehavior.manual
})

// 数据量很多的时候使用 builder 构建。
ListView.builder({
  Key key, 
  Axis scrollDirection: Axis.vertical, 
  bool reverse: false, 
  ScrollController controller, 
  bool primary, 
  ScrollPhysics physics, 
  bool shrinkWrap: false, 
  EdgeInsetsGeometry padding, 
  double itemExtent, 
  @required IndexedWidgetBuilder itemBuilder, // 子元素渲染构造器
  int itemCount, // 列表中元素的数量
  bool addAutomaticKeepAlives: true, 
  bool addRepaintBoundaries: true, 
  bool addSemanticIndexes: true, 
  double cacheExtent, 
  int semanticChildCount, 
  DragStartBehavior dragStartBehavior: DragStartBehavior.start
})

ListView.custom({
  Key key, 
  Axis scrollDirection: Axis.vertical, 
  bool reverse: false, 
  ScrollController controller, 
  bool primary, 
  ScrollPhysics physics, 
  bool shrinkWrap: false, 
  EdgeInsetsGeometry padding, 
  double itemExtent, 
  @required SliverChildDelegate childrenDelegate, 
  double cacheExtent, 
  int semanticChildCount
})

// 展示列表分割线
ListView.separated({
  Key key, 
  Axis scrollDirection: Axis.vertical, 
  bool reverse: false, 
  ScrollController controller, 
  bool primary, 
  ScrollPhysics physics, 
  bool shrinkWrap: false, 
  EdgeInsetsGeometry padding, 
  @required IndexedWidgetBuilder itemBuilder, 
  @required IndexedWidgetBuilder separatorBuilder, // 分割线渲染构造器
  @required int itemCount, 
  bool addAutomaticKeepAlives: true, 
  bool addRepaintBoundaries: true, 
  bool addSemanticIndexes: true, 
  double cacheExtent, 
  ScrollViewKeyboardDismissBehavior keyboardDismissBehavior: ScrollViewKeyboardDismissBehavior.manual
})
```

# 示例

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  final List<Widget> list = <Widget>[
    new ListTile(
      title: Text('titletitletitletitletitletitletitletitletitletitletitletitletitletitle',style: new TextStyle(fontWeight: FontWeight.w400,fontSize: 18.0),),
      subtitle: Text('Test Test Test Test Test Test Test Test Test Test Test Test Test Test Test Test Test '),
      leading: Icon(Icons.fastfood,color: Colors.blue,),
    ),
    new ListTile(
      title: Text('data',style: new TextStyle(fontWeight: FontWeight.w400,fontSize: 18.0),),
      subtitle: Text('data'),
      leading: Icon(Icons.fastfood,color: Colors.blue,),
    ),
  ];

  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(
          title: Text('data'),
        ),
        body: new Center(
          child: new ListView(
            children: list,
          )
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/52.png" width = "25%" height = "25%"/>