
# Center(居中布局)
Center(居中布局)： 子元素处于水平和垂直方向的中间位置。

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
          title: Text('Title'),
        ),
        body: new Center(
          child: new Text('Center Layout'),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/29.png" width = "25%" height = "25%"/>