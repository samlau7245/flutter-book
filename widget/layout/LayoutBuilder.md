
# LayoutBuilder(布局构造器)

`LayoutBuilder`可以通过判断设备尺寸来布局界面。与其类似的用法还有`MediaQuery.of(context).orientation == Orientation.portrait`

* [LayoutBuilder Class](https://api.flutter.dev/flutter/widgets/LayoutBuilder-class.html)

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      home: new Scaffold(
        appBar: AppBar(
          title: Text('FittedBox Demo'),
        ),
        body: LayoutBuilder(
          builder: (BuildContext context, BoxConstraints constraints) {
            // 通过 constraints 来判断屏幕的尺寸，从而进行界面适配。
            if (constraints.maxWidth < 100) {
            } else {}
            return Center();
          },
        ),
      ),
    );
  }
}
```
