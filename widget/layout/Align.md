# Align(对齐布局)
Align(对齐布局)： 将子组件按照指定的方式对齐，并且根据子组件的大小调整自己的大小。

* [Align (Flutter Widget of the Week)](https://www.youtube.com/watch?v=g2E7yl3MwMk)

|属性|值|描述|
| --- | --- | --- | --- |
|bottomCenter|(0.5,1.0)|底部中心|
|bottomLeft|(0.0,1.0)|左下角|
|bottomRight|(1.0,1.0)|右下角|
|center|(0.5,0.5)|水平垂直居中|
|centerLeft|(0.0,0.5)|坐边缘中心|
|centerRight|(1.0,0.5)|右边缘中心|
|topCenter|(0.5,0.0)|顶部中心|
|topLeft|(0.0,0.0)|左上角|
|topRight|(1.0,0.0)|右上角|

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
      body: new Stack(
        children: <Widget>[
          // 左上角
          new Align(
            alignment: new FractionalOffset(0.0, 0.0),
            child: new Image.asset('icons/code.png',width: 128.0,height: 128.0,),
          ),
          // 右上角
          new Align(
            alignment: FractionalOffset(1.0, 0.0),
            child: new Image.asset('icons/code.png',width: 128.0,height: 128.0,),
          ),
          // 水平垂直居中
          new Align(
            alignment: FractionalOffset.center,
            child: new Image.asset('icons/code.png',width: 128.0,height: 128.0,),
          ),
          // 左下角
          new Align(
            alignment: FractionalOffset.bottomLeft,
            child: new Image.asset('icons/code.png',width: 128.0,height: 128.0,),
          ),
          // 右下角
          new Align(
            alignment: FractionalOffset.bottomRight,
            child: new Image.asset('icons/code.png',width: 128.0,height: 128.0,),
          ),
        ],
      ),
    );
  }
}
```

<img src="/assets/images/flutter/31.png" width = "25%" height = "25%"/>