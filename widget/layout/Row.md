
* [Row class](https://api.flutter.dev/flutter/widgets/Row-class.html)

# 构造函数

```dart
Row({
  Key key,
  MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start,
  MainAxisSize mainAxisSize = MainAxisSize.max,
  CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center,
  TextDirection textDirection,
  VerticalDirection verticalDirection = VerticalDirection.down,
  TextBaseline textBaseline,
  List<Widget> children = const <Widget>[],
})
```

> **[info] 构造函数中的参数含义**
>
> 可以参数`Column`布局。

<img src="/assets/images/flutter/74.png" />

<img src="/assets/images/flutter/75.png" />

<img src="/assets/images/flutter/76.png" />

# 示例

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

<img src="/assets/images/flutter/32.png"/>

## 实现一个简单的分割线

```dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceAround,
  children: <Widget>[
    Expanded(
      child: Container(
        margin: EdgeInsets.only(left: 20),
        color: Color(0xffEAEAEA),
        height: 1,
      ),
      flex: 1,
    ),
    Expanded(
      child: Container(
        child: Center(
          child: Text(
            '其他登陆方式',
            style: TextStyle(fontSize: 12, color: Color(0xff999999)),
          ),
        ),
      ),
      flex: 1,
    ),
    Expanded(
      child: Container(
        margin: EdgeInsets.only(right: 20),
        color: Color(0xffEAEAEA),
        height: 1,
      ),
      flex: 1,
    ),
  ],
)
```

<img src="/assets/images/widgets/42.png" /> 
