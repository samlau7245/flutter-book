
* [Stack Class](https://api.flutter.dev/flutter/widgets/Stack-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/liEGSeD3Zt8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
Stack({
  Key key,
  AlignmentGeometry alignment: AlignmentDirectional.topStart,
  TextDirection textDirection,
  StackFit fit: StackFit.loose,
  Overflow overflow: Overflow.clip,
  List<Widget> children: const []
})

enum StackFit {
  loose,
  expand,
  passthrough,
}

enum Overflow {
  visible, // 保留溢出
  clip, // 删除溢出
}

enum TextDirection {
  rtl, // 左
  ltr, // 右
}
```

<img src="/assets/images/flutter/67.gif"/>

# 示例

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

# IndexedStack

[IndexedStack Class](https://api.flutter.dev/flutter/widgets/IndexedStack-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/_O0PPD1Xfbk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<img src="/assets/images/flutter/68.gif"/>

`IndexedStack`继承了`Stack`，它的作用就是显示第`index`个`child`，其他的`child`不可见。所以`IndexStack`的尺寸永远是和最大的子节点尺寸一致的。

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var stack = new IndexedStack(
      index: 1,
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

<img src="/assets/images/flutter/45.png" width = "25%" height = "25%"/>