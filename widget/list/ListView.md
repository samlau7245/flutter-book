
[ListView Class](https://api.flutter.dev/flutter/widgets/ListView-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/KJpkjHGiI5A" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

## ListView

```dart
ListView({
  Key key, 
  List<Widget> children: const [], 
  
  double itemExtent, // 子元素长度。当列表中的每一项长度是固定的情况下可以指定该值，有助于提高列表的性能
  double cacheExtent, // 预渲染区域长度
  int semanticChildCount, 

  bool shrinkWrap: false, // 决定列表的长度是否仅包裹其内容的长度。当ListView嵌在一个无限长的容器组件中时，shrinkWrap必须为true，否则Flutter会给出警告
  bool primary, 
  bool reverse: false, 
  bool addAutomaticKeepAlives: true, 
  bool addRepaintBoundaries: true, 
  bool addSemanticIndexes: true, 
  
  DragStartBehavior dragStartBehavior: DragStartBehavior.start, 
  ScrollViewKeyboardDismissBehavior keyboardDismissBehavior: ScrollViewKeyboardDismissBehavior.manual
  EdgeInsetsGeometry padding, // 列表内边距
  Axis scrollDirection: Axis.vertical, // 列表的滚动方向
  ScrollController controller, // 控制器，与列表滚动相关，比如监听列表的滚动事件
  ScrollPhysics physics,  // 列表滚动至边缘后继续拖动的物理效果，Android与iOS效果不同。
})

```

## ListView.builder

```dart
// 数据量很多的时候使用 builder 构建。
ListView.builder({
  Key key, 
  @required IndexedWidgetBuilder itemBuilder, // 子元素渲染构造器

  Axis scrollDirection: Axis.vertical, 
  ScrollController controller, 
  ScrollPhysics physics, 
  EdgeInsetsGeometry padding, 
  DragStartBehavior dragStartBehavior: DragStartBehavior.start

  double itemExtent, 
  double cacheExtent, 
  int itemCount, // 列表中元素的数量
  int semanticChildCount, 

  bool reverse: false, 
  bool primary, 
  bool shrinkWrap: false, 
  bool addAutomaticKeepAlives: true, 
  bool addRepaintBoundaries: true, 
  bool addSemanticIndexes: true, 
})
```

## ListView.custom

```dart
ListView.custom({
  Key key, 
  @required SliverChildDelegate childrenDelegate, 
  
  bool reverse: false, 
  bool primary, 
  bool shrinkWrap: false, 

  double itemExtent, 
  double cacheExtent, 
  int semanticChildCount

  Axis scrollDirection: Axis.vertical, 
  ScrollController controller, 
  ScrollPhysics physics, 
  EdgeInsetsGeometry padding, 
})
```

## ListView.separated

```dart
// 展示列表分割线
ListView.separated({
  Key key, 
  
  @required IndexedWidgetBuilder itemBuilder, 
  @required IndexedWidgetBuilder separatorBuilder, // 分割线渲染构造器
  @required int itemCount,

  bool reverse: false, 
  bool primary, 
  bool addAutomaticKeepAlives: true, 
  bool addRepaintBoundaries: true, 
  bool shrinkWrap: false, 
  bool addSemanticIndexes: true, 

  double cacheExtent, 

  Axis scrollDirection: Axis.vertical, 
  ScrollViewKeyboardDismissBehavior keyboardDismissBehavior: ScrollViewKeyboardDismissBehavior.manual
  ScrollController controller, 
  ScrollPhysics physics, 
  EdgeInsetsGeometry padding,  
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

## 分割线

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text("刷新"),
    ),
    body: ListView.separated(
      itemBuilder: (_, index) {
        return Container(
          height: 50,
          child: Center(child: Text("data-$index")),
        );
      },
      separatorBuilder: (_, index) {
        return Divider(
          height: .5,
          //indent: 75, 
          color: Color(0xFFDDDDDD),
        );
      },
      itemCount: 20,
    ),
  );
}
```

<img src="/assets/images/widgets/64.png"/>
