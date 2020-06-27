
# PopupMenuButton(弹出菜单组件)

| 属性|类型|说明|
| --- | --- | --- |
|child|Widget||
|icon|Icon||
|itemBuilder|`PopupMenuItembuilder<T>`|菜单构造器，菜单项为任意类型，文本、图标都行|
|onSelected|`PopupMenuItembuilder<T>`|菜单被选中的回调方法|

[示例代码](https://codepen.io/samlau7245/pen/xxwaZYO)

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "FloatingActionButton Demo",
      home: HomePage(),
    );
  }
}

//////////////////////////////首页//////////////////////////////////

class HomePage extends StatefulWidget {
  HomePage({Key key}) : super(key: key);
  @override
  _HomePage createState() => new _HomePage();
}

enum ConferenceItem { AddMember, LockConference, ModifyLayout, TurnoffAll }

class _HomePage extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("FloatingActionButton Demo"),
        actions: <Widget>[
          PopupMenuButton<ConferenceItem>(itemBuilder: (_) {
            return <PopupMenuEntry<ConferenceItem>>[
              const PopupMenuItem<ConferenceItem>(
                child: Text('添加成员'),
                value: ConferenceItem.AddMember,
              ),
              const PopupMenuItem<ConferenceItem>(
                child: Text('锁定会议'),
                value: ConferenceItem.LockConference,
              ),
              const PopupMenuItem<ConferenceItem>(
                child: Text('修改布局'),
                value: ConferenceItem.ModifyLayout,
              ),
              const PopupMenuItem<ConferenceItem>(
                child: Text('挂断所有'),
                value: ConferenceItem.TurnoffAll,
              ),
            ];
          })
        ],
      ),
    );
  }
}
```

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
            child: PopupMenuButton<ConferenceItem>(
              itemBuilder: (BuildContext context) {
                return <PopupMenuEntry<ConferenceItem>>[
                  const PopupMenuItem<ConferenceItem>(
                    child: Text('添加成员'),
                    value: ConferenceItem.AddMember,
                  ),
                  const PopupMenuItem<ConferenceItem>(
                    child: Text('锁定会议'),
                    value: ConferenceItem.LockConference,
                  ),
                  const PopupMenuItem<ConferenceItem>(
                    child: Text('修改布局'),
                    value: ConferenceItem.ModifyLayout,
                  ),
                  const PopupMenuItem<ConferenceItem>(
                    child: Text('挂断所有'),
                    value: ConferenceItem.TurnoffAll,
                  ),
                ];
              },
              onSelected: (ConferenceItem item) {
              },
            ),
          ),
        ),
      ),
    );
  }
}

enum ConferenceItem { AddMember, LockConference, ModifyLayout, TurnoffAll }
```

<img src="/assets/images/flutter/22.gif"/>
