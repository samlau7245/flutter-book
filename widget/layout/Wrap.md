
# Wrap(按宽高自动换行布局)

`Wrap` 使用了`Flex`中的一些概念，某种意义上和`Row`、`Column`更加相似。单行的`Wrap`和`Row`表现几乎一致，单列的`Wrap`和`Column`表现几乎一致。`Wrap`是在主轴上空间不足时，则向次轴上去扩展显示。

* [Wrap Class](https://api.flutter.dev/flutter/widgets/Wrap-class.html)

|属性|类型|默认值|描述|
| --- | --- | --- | --- |
|direction|Axis|Axis.horizontal|主轴(mainAxis)的方向,默认为水平|
|alignment|WrapAlignment||主轴方向上的对齐方式,默认为start|
|spacing|double|0.0|主轴方向上的间距|
|runAlignment| WrapAlignment| wrapAlignment.start|run的对齐方式。run可以理解为新的行或者列,如果是水平方向布局的话,run可以理解为新的一行|
|runSpacing|double|0.0|run的间距|
|crossAxisAlignment| WrapCrossAlignment wrapCrossAlignment.start|主轴(crossAxis)方向上的对齐方式|
|textDirecfion|TextDirection||文本方向|
|verticalDirection| VerticalDirection|定义了children摆放顺序,默认是down|

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
