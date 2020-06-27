
# SizedBox(设置具体尺寸)

`SizedBox`组件是一个特定大小的盒子，这个组件强制他的child有特定的宽度和高度。

|属性|类型|描述|
| --- | --- | --- |
|width|double|如果具体设置了宽度，则强制child宽度为此值； 如果没有设置，则根据child宽度调整自身宽度|
|height|double|如果具体设置了高度，则强制child高度为此值； 如果没有设置，则根据child高度调整自身宽度|

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Demo',
      home: new Scaffold(
        appBar: new AppBar(
          title: Text('data'),
        ),
        body: SizedBox(
          width: 200.0,
          height: 300.0,
          child: const Card(
            child: Text(
              'data',
              style: TextStyle(fontSize: 36.0),
            ),
          ),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/47.png" width = "25%" height = "25%"/>
