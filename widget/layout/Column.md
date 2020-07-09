
* [Column class](https://api.flutter.dev/flutter/widgets/Column-class.html)

# 构造函数

```dart
Column({
  Key key,
  MainAxisAlignment mainAxisAlignment: MainAxisAlignment.start, // 主轴的排列方式
  MainAxisSize mainAxisSize: MainAxisSize.max, // 主轴应该占据多少空间。取值max为最大，min为最小。
  CrossAxisAlignment crossAxisAlignment: CrossAxisAlignment.center, // 交叉轴的排列方式
  TextDirection textDirection,
  VerticalDirection verticalDirection: VerticalDirection.down,
  TextBaseline textBaseline,
  List<Widget> children: const []
});

enum MainAxisAlignment {
  // 把 children 放置在尽可能靠近主轴起点的位置。
  // 如果在水平(horizontal)方向上使用`MainAxisAlignment.start`,则需要使用`TextDirection`来确定起点是左侧还是右侧。
  // 如果在垂直(vertical)方向上使用`MainAxisAlignment.start`,则需要使用`VerticalDirection`来确定起点是顶部还是底部。
  start, 
  end, // 把 children 放置在尽可能靠近主轴末端的位置。
  center, // 把 children 放置在尽可能靠近主轴中心的位置。
  spaceBetween, // 将主轴方向上的空白区域均分，使得children之间的空白区域相等，首尾child都靠近首尾，没有间隙。
  spaceAround, // 将主轴方向上的空白区域均分，使得children之间的空白区域相等，但是首尾child的空白区域为1/2。
  spaceEvenly, // 将主轴方向上的空白区域均分，使得children之间的空白区域相等，包括首尾child。
}

enum MainAxisSize {
  min,
  max,
}

enum CrossAxisAlignment {
  start, // children在交叉轴上起点处展示。
  end, // children在交叉轴上末尾展示。
  center, // children在交叉轴上居中展示。
  stretch, // 让children填满交叉轴方向。
  baseline, // 在交叉轴方向，使得children的baseline对齐。
}

enum TextDirection {
  rtl, // 左
  ltr, // 右
}

enum VerticalDirection {
  up, // 上
  down, // 下
}

enum TextBaseline {
  alphabetic,
  ideographic,
}
```

## MainAxisAlignment 

<img src="/assets/images/widgets/03.png"/>

## CrossAxisAlignment

<img src="/assets/images/widgets/04.png"/>

# 示例

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Demo',
      home: PaddingDemo(),
    );
  }
}

class PaddingDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: Text('Align Demo'),
      ),
      body: new Column(
        crossAxisAlignment: CrossAxisAlignment.start,// 水平方向靠左对齐
        mainAxisSize: MainAxisSize.min, //主轴方向最小化处理
        children: <Widget>[
          new Text('度权重查询 SEO概况查询 友情链接查询 Google PR查询 Whois信息查询 域名备案查询'),
          new Text('度权重查询 SEO概况查询 友情链接查询 Google PR查询 Whois信息查询 域名备案查询'),
          new Text('度权重查询 SEO概况查询 友情链接查询 Google PR查询 Whois信息查询 域名备案查询'),
          new Text('data1'),
          new Text('度权重查询 SEO概况查询 友情链接查询 Google PR查询 Whois信息查询 域名备案查询'),
          new Text('度权重查询 SEO概况查询 友情链接查询 Google PR查询 Whois信息查询 域名备案查询度权重查询 SEO概况查询 友情链接查询 Google PR查询 Whois信息查询 域名备案查询'),
        ],
      ),
    );
  }
}
```

<img src="/assets/images/flutter/34.png" width = "25%" height = "25%"/>
