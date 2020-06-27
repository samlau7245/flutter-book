# SnackBar(轻量提示组件)

| 属性|类型|说明|
| --- | --- | --- |
|action|||
|animation|||
|content|||
|duration|||
|backgroundColor|||

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
          child: new Builder(builder:(BuildContext context) {
            return new FlatButton(onPressed: (){
              Scaffold.of(context).showSnackBar(
                new SnackBar(content: new Text('data'))
              );
            }, child: new Text('data'));
          })
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/25.gif"/>
