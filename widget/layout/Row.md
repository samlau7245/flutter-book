
# Row(水平布局)
Row(水平布局) 用来完成子组件在水平方向的排列。

<img src="/assets/images/flutter/74.png" width = "50%" height = "50%"/>

<img src="/assets/images/flutter/75.png" width = "50%" height = "50%"/>

|属性|值|描述|
| --- | --- | --- | --- |
|mainAxisAlignment|MainAxisAlignment|主轴的排列方式|
|crossAxisAlignment|CrossAxisAlignment|次轴的排列方式|
|mainAxisSize|MainAxisSize|主轴应该占据多少空间。取值max为最大，min为最小。|
|children|`List<Widget>`||

<img src="/assets/images/flutter/76.png" width = "50%" height = "50%"/>

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var stars = Row(
      mainAxisSize: MainAxisSize.min,
      children: [
        Icon(Icons.star, color: Colors.green[500]),
        Icon(Icons.star, color: Colors.green[500]),
        Icon(Icons.star, color: Colors.green[500]),
        Icon(Icons.star, color: Colors.black),
        Icon(Icons.star, color: Colors.black),
      ],
    );
    final ratings = Container(
      color: Colors.blue,
      padding: EdgeInsets.all(20),
      child: Row(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly, //空间均分
        children: [
          stars,
          Text(
            '170 Reviews',
            style: TextStyle(
              color: Colors.black,
              fontWeight: FontWeight.w800,
              fontFamily: 'Roboto',
              letterSpacing: 0.5,
              fontSize: 20,
            ),
          ),
        ],
      ),
    );

    return MaterialApp(
      title: 'Flutter Demo',
      home: new Scaffold(
        appBar: AppBar(
          title: Text('FittedBox Demo'),
        ),
        body: Center(
          child: ratings,
        ),
      ),
    );
  }
}

```

<img src="/assets/images/flutter/32.png" width = "25%" height = "25%"/>
