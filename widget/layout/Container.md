
[Container class](https://api.flutter.dev/flutter/widgets/Container-class.html)

Container(基础布局)是一个组合的 Widget 。类似于HTML中的`<span>`标签，用于组合其他的 Widget 。

<iframe width="560" height="315" src="https://www.youtube.com/embed/c1xLMaTUWCY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
Container({
  Key key,
  AlignmentGeometry alignment, // 控制 child 的对齐方式，如果 Container或者 Container父节点尺寸大于 child 的尺寸，这个属性设置会起作用，有很多种对齐方式
  EdgeInsetsGeometry padding, // 填充属性， Decoration **内部**的空白区域，如果有 child的话，child位于padding 内部
  Color color, // 用来设置 Container背景色，如果 foregroundDecoration 设置的话，可能会遮盖 color效果
  Decoration decoration, // 给Container添加一些装饰，比如形状、颜色...，设置了 Decoration 的话，就不能设置 color属性，否则会报错，此时应该在 Decoration 中进行颜色的设置
  Decoration foregroundDecoration, // 绘制在 child前面的装饰
  double width,
  double height,
  BoxConstraints constraints, // 添加到 child上额外的约束条件
  EdgeInsetsGeometry margin, // 边距属性，围绕在 Decoration 和 child 之外的空白区域，不属于内容区域
  Matrix4 transform, // 设置 Container 的变换矩阵，类型为 Matrix4
  Widget child,
  Clip clipBehavior: Clip.none
)}
```

# 示例

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: new Scaffold(
        appBar: new AppBar(
          title: new Text("AppBar Title"),
        ),
        body: new Center(
          child: new Container(
            width: 200,
            height: 200,
            decoration: BoxDecoration(
              color: Colors.red
            ),
            child: new Center(
              child: new Text('Container Text'),
            ),
          ),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/02.png" width = "25%" height = "25%"/>

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Widget container = new Container(
      // 添加装饰效果
      decoration: new BoxDecoration(
        color: Colors.grey,
      ),
      // 子元素指定为一个垂直水平嵌套布局的组件
      child: new Column(
        children: <Widget>[
          // 第一行
          new Row(
            children: <Widget>[
              new Expanded(
                child: new Container(
                width: 150.0,
                height: 150.0,
                // 添加边框样式
                decoration: new BoxDecoration(
                    border: new Border.all(
                      width: 10.0,
                      color: Colors.blueGrey,
                    ),
                    borderRadius: const BorderRadius.all(
                      const Radius.circular(8.0),
                    )),
                margin: const EdgeInsets.all(4.0),
                child: new Image.asset('icons/code.png'),
              )),
              new Expanded(
                child: new Container(
                width: 150.0,
                height: 150.0,
                decoration: new BoxDecoration(
                    border: new Border.all(
                      width: 10.0,
                      color: Colors.blueGrey,
                    ),
                    borderRadius: const BorderRadius.all(
                      const Radius.circular(8.0),
                    )),
                margin: const EdgeInsets.all(4.0),
                child: new Image.asset('icons/code.png'),
              )),
            ],
          ),
          // 第二行
          new Row(
            children: <Widget>[
              new Expanded(
                  child: new Container(
                width: 150.0,
                height: 150.0,
                decoration: new BoxDecoration(
                    border: new Border.all(
                      width: 10.0,
                      color: Colors.blueGrey,
                    ),
                    borderRadius: const BorderRadius.all(
                      const Radius.circular(8.0),
                    )),
                margin: const EdgeInsets.all(4.0),
                child: new Image.asset('icons/code.png'),
              )),
              new Expanded(
                  child: new Container(
                width: 150.0,
                height: 150.0,
                decoration: new BoxDecoration(
                    border: new Border.all(
                      width: 10.0,
                      color: Colors.blueGrey,
                    ),
                    borderRadius: const BorderRadius.all(
                      const Radius.circular(8.0),
                    )),
                margin: const EdgeInsets.all(4.0),
                child: new Image.asset('icons/code.png'),
              )),
            ],
          )
        ],
      ),
    );

    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(
          title: Text('Title'),
        ),
        body: container,
      ),
    );
  }
}
```

<img src="/assets/images/flutter/28.png"/>
