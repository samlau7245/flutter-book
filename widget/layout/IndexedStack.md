# [IndexedStack](https://www.youtube.com/watch?v=_O0PPD1Xfbk)

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