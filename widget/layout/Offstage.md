
# Offstage(控制是否显示组件)

`Offstage` 通过参数来控制child是否显示。

|属性|类型|默认值|描述|
| --- | --- | --- |--- |
|offstage|bool|true|true：不显示|

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final appTitle = "Offstage 控制是否展示组件示例";
    return new MaterialApp(
      title: 'Demo',
      home: new MyHomePage(title: appTitle,),
    );
  }
}

class MyHomePage extends StatefulWidget {
  final String title;
  MyHomePage({Key key, this.title}) : super(key: key);

  @override
  _MyHomePage createState() => _MyHomePage();
}

class _MyHomePage extends State<MyHomePage> {
  bool offstage = true;
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text(widget.title),
      ),
      body: new Center(
        child: new Offstage(
          offstage: offstage,
          child: new Text(
            'Show Stage',
            style: TextStyle(fontSize: 36.0),
          ),
        ),
      ),
      floatingActionButton: new FloatingActionButton(
        onPressed: () {
          setState(() {
            offstage = !offstage;
          });
        },
        child: new Icon(Icons.flip),
      ),
    );
  }
}
```
<img src="/assets/images/flutter/55.gif"/>
