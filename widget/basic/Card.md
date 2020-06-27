# [Card(卡片组件)](https://api.flutter.dev/flutter/material/Card-class.html)

Card(卡片组件)内容可以由大多数类型的`Widget`构成，但通常与`ListTitle`搭配使用。`Card`有一个`child`属性，可以支持多个`child`的列、行、列表、网格或者其他小部件。默认情况下`Card`将其大小缩放为`0`像素。你可以使用`SizeBox`组件来限制`Card`的大小。

| 属性|类型|说明|
| --- | --- | --- |
|child|Widget||
|margin|||
|shape|ShapeBorder||

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var card = new SizedBox(
      height: 250.0,
      child: new Card(
        child: new Column(
          children: <Widget>[
            new ListTile(
              title: Text('data1'),
              subtitle: Text('2020动画《真人快打传奇：蝎子的复仇》1080p.HD中英双字[04-14]2019动画《红鞋子和七个小矮人》1080p.HD中英双字'),
              leading: Icon(Icons.home),
            ),
            new Divider(),
            new ListTile(
              title: Text('data2'),
              subtitle: Text('2020动画《真人快打传奇：蝎子的复仇》1080p.HD中英双字[04-14]2019动画《红鞋子和七个小矮人》1080p.HD中英双字'),
              leading: Icon(Icons.school),
            ),
          ],
        ),
      ),
    );

    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(
          title: Text('Title'),
        ),
        body: new Center(
          child: card,
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/27.png"/>