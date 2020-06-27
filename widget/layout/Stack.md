
# Stack(栈布局-将Widget覆盖在另一个的上面)

## Alignment

`Stack`组件的每个子组件要么定位，要么不定位。定位的子组件用`Positioned`组件包裹。`Stack`组件本身包含所有不定位的子组件，子组件根据`alignment`属性进行定位(默认为左上角)。然后根据定位的子组件的`top`、`right`、`bottom`和`left`属性将它们位置在`Stack`组件上。

|属性|类型|默认值|描述|
| --- | --- | --- | --- |
|alignment|AlignmentGeometry|Alignment.topLeft|定位位置有以下几种：<br>`bottomCenter` : 底部中心 <br>`bottomLeft` : 左下角 <br>`bottomRight` : 右下角 <br>`center` : 水平垂直居中 <br>`centerLeft` : 坐边缘中心 <br>`centerRight` : 右边缘中心 <br>`topCenter` : 顶部中心 <br>`topLeft` : 左上角 <br>`topRight` : 右上角|

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var stack = new Stack(
      alignment: Alignment.topLeft,
      children: <Widget>[
        new CircleAvatar(
          backgroundImage: new AssetImage('icons/code.png'),
          radius: 100.0,
        ),
        new Container(
          decoration: new BoxDecoration(
            color: Colors.blue,
          ),
          child: new Text(
            'TestTes',
            style: new TextStyle(
              fontSize: 30.0,
              fontWeight: FontWeight.bold,
              color: Colors.white,
            ),
          ),
        )
      ],
    );

    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(title: Text('data'),),
        body: new Center(
          child: stack,
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/43.png"/>
<!-- width = "25%" height = "25%" -->

## Overflow

```dart
enum Overflow {
  visible,/// Overflowing children will be visible.
  clip,/// Overflowing children will be clipped to the bounds of their parent.
}
```

<img src="/assets/images/flutter/67.gif"/>

## Positioned

`Positioned`组件是用来定位的。`Stack`组件里需要包裹一个定位组件。

|属性|类型|描述|
| --- | --- | --- |
|top|double|子元素相对顶部边界距离|
|bottom|double|子元素相对底部边界距离|
|left|double|子元素相对坐侧边界距离|
|right|double|子元素相对右侧边界距离|

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var stack = new Stack(
      alignment: Alignment.topLeft,
      children: <Widget>[
        new CircleAvatar(
          backgroundImage: new AssetImage('icons/code.png'),
          radius: 100.0,
        ),
        new Positioned(
            bottom: 50.0,
            right: 50.0,
            child: new Text('data',
                style: new TextStyle(
                    fontSize: 36.0,
                    fontWeight: FontWeight.bold,
                    color: Colors.red))),
      ],
    );

    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(
          title: Text('data'),
        ),
        body: new Center(
          child: stack,
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/44.png"/>

