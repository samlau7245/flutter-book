
[Wrap Class](https://api.flutter.dev/flutter/widgets/Wrap-class.html):按宽高自动换行布局

<iframe width="560" height="315" src="https://www.youtube.com/embed/z5iw2SeFx2M" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<img src="/assets/images/widgets/40.gif"/>

# 构造函数

```dart
Wrap({
  Key key,
  Axis direction: Axis.horizontal, // 主轴(mainAxis)的方向,默认为水平
  WrapAlignment alignment: WrapAlignment.start, // 主轴方向上的对齐方式,默认为start
  double spacing: 0.0, // 主轴方向上的间距
  WrapAlignment runAlignment: WrapAlignment.start, // run的对齐方式。run可以理解为新的行或者列,如果是水平方向布局的话,run可以理解为新的一行
  double runSpacing: 0.0, // run的间距
  WrapCrossAlignment crossAxisAlignment: WrapCrossAlignment.start, // 主轴(crossAxis)方向上的对齐方式
  TextDirection textDirection, // 文本方向
  VerticalDirection verticalDirection: VerticalDirection.down, // 定义了children摆放顺序,默认是down
  List<Widget> children: const [] 
})

enum Axis {
  horizontal,
  vertical,
}

enum WrapAlignment {
  start,
  end,
  center,
  spaceBetween,
  spaceAround,
  spaceEvenly,
}
```
`Wrap` 使用了`Flex`中的一些概念，某种意义上和`Row`、`Column`更加相似。单行的`Wrap`和`Row`表现几乎一致，单列的`Wrap`和`Column`表现几乎一致。`Wrap`是在主轴上空间不足时，则向次轴上去扩展显示。


# 示例

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(
          title: new Text('Demo'),
        ),
        body: Wrap(
          spacing: 8.0, //主轴间距
          runSpacing: 4.0, // 行间距【默认水平排序】
          children: <Widget>[
            Chip(
              label: new Text('data'),
              avatar: CircleAvatar(
                backgroundColor: Colors.lightGreen.shade800,
                child: new Text(
                  'data',
                  style: new TextStyle(fontSize: 10.0),
                ),
              ),
            ),
            Chip(
              label: new Text('datadata'),
              avatar: CircleAvatar(
                backgroundColor: Colors.lightGreen.shade800,
                child: new Text(
                  'datadata',
                  style: new TextStyle(fontSize: 10.0),
                ),
              ),
            ),
            Chip(
              label: new Text('datadatadatadata'),
              avatar: CircleAvatar(
                backgroundColor: Colors.lightGreen.shade800,
                child: new Text(
                  'datadatadatadata',
                  style: new TextStyle(fontSize: 10.0),
                ),
              ),
            ),
            Chip(
              label: new Text('datadatadatadataadatadata'),
              avatar: CircleAvatar(
                backgroundColor: Colors.lightGreen.shade800,
                child: new Text(
                  'datadatadatadataadatadata',
                  style: new TextStyle(fontSize: 10.0),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/56.png" width = "50%" height = "50%"/>
