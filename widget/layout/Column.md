
# Column(垂直布局)
Column(垂直布局) 用来完成对子组件纵向的排列。主轴是垂直方向，次轴是水平方向。

|属性|值|描述|
| --- | --- | --- | --- |
|mainAxisAlignment|MainAxisAlignment|主轴的排列方式|
|crossAxisAlignment|CrossAxisAlignment|次轴的排列方式|
|mainAxisSize|MainAxisSize|主轴应该占据多少空间。取值max为最大，min为最小。|
|children|`List<Widget>`||

```dart
Column({
  Key key,
  MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start,
  CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center,

  MainAxisSize mainAxisSize = MainAxisSize.max,
  TextDirection textDirection,
  VerticalDirection verticalDirection = VerticalDirection.down,
  TextBaseline textBaseline,
  List<Widget> children = const <Widget>[],
})
```

<img src="/assets/images/flutter/77.png" width = "50%" height = "50%"/>

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
        children: <Widget>[
          new Expanded(
            child: new Text('data', textAlign: TextAlign.center,),
          ),
          new Expanded(
            child: new Text('data', textAlign: TextAlign.center,),
          ),
          new Expanded(
            child: new FittedBox(
              fit: BoxFit.contain,
              child: const FlutterLogo(),
            )
          ),
        ],
      ),
    );
  }
}
```

<img src="/assets/images/flutter/33.png" width = "25%" height = "25%"/>

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
