
# [FlatButton(扁平按钮组件)](https://api.flutter.dev/flutter/material/FlatButton-class.html)
`FlatButton`组件是`Materail Design`风格按钮，点击时会有一个阴影效果。

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
          title: Text('Demo'),
        ),
        body: new Center(
          child: FlatButton(
              onPressed: () {},
              child: Text(
                'FlatButton',
                style: TextStyle(fontSize: 24.0),
              )),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/21.gif"/>