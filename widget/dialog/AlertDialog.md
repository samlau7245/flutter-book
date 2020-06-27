
# AlertDialog(提示对话框组件)

[示例](https://codepen.io/samlau7245/pen/zYvJLpm)

| 属性|类型|说明|
| --- | --- | --- |
|actions|`List<Widget>`||
|title|||
|contentPadding|||
|content|Widget|内容，如果内容比较多可以用`SingleChildScrollView`组件进行包裹|
|titlePadding|||

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
          child: new Builder(builder: (BuildContext context){
            return new FlatButton(onPressed: (){
              _neverSatisfied(context);
            }, child: new Text('data'));
          }),
        ),
      ),
    );
  }
}

Future _neverSatisfied(BuildContext context) async {
  return showDialog(
      context: context,
      barrierDismissible: false,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Rewind and remember'),
          content: SingleChildScrollView(
            child: ListBody(
              children: <Widget>[
                Text('You will never be satisfied.'),
                Text('You\’re like me. I’m never satisfied.'),
              ],
            ),
          ),
          actions: <Widget>[
            FlatButton(
              child: Text('Regret'),
              onPressed: () {
                Navigator.of(context).pop();
              },
            ),
          ],
        );
      });
}

```

<img src="/assets/images/flutter/24.gif"/>