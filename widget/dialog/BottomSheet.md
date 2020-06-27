
# [BottomSheet](https://api.flutter.dev/flutter/material/BottomSheet-class.html)

BottomSheet有两种设计方式：

* `Persistent` : 这是用过[ScaffoldState.showBottomSheet](https://api.flutter.dev/flutter/material/ScaffoldState/showBottomSheet.html)来展示。
* `Modal` 通过[showModalBottomSheet](https://api.flutter.dev/flutter/material/BottomSheet-class.html)来展示。

[示例代码](https://codepen.io/samlau7245/pen/ZEbMMpP)

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(title: "Demo", home: HomePage());
  }
}

class HomePage extends StatefulWidget {
  HomePage({Key key}) : super(key: key);
  @override
  _HomePage createState() => new _HomePage();
}

class _HomePage extends State<HomePage> {
  final GlobalKey<ScaffoldState> scaffoldKey = GlobalKey<ScaffoldState>();
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      key: scaffoldKey,
      body: Builder(
        builder: (BuildContext context) => Center(
          child: FlatButton(
            child: Text("Alert"),
            onPressed: () {
              _showBottomSheetDemo(context);
            },
          ),
        ),
      ),
      // floatingActionButton: FloatingActionButton(
      //   child: Text("Alert"),
      //   onPressed: () {
      //     scaffoldKey.currentState.showBottomSheet<void>(
      //       (_) {
      //         return Container(
      //           margin: const EdgeInsets.all(40.0),
      //           child: const Text('BottomSheet'),
      //         );
      //       },
      //     );
      //   },
      // ),
    );
  }

  void _showBottomSheetDemo(BuildContext context) {
    Scaffold.of(context).showBottomSheet((_) {
      return Container(
        height: 200.0,
        color: Color(0xFF37966F),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          mainAxisSize: MainAxisSize.min,
          children: <Widget>[
            const Text('BottomSheet'),
            RaisedButton(
              child: const Text('Close BottomSheet'),
              onPressed: () => Navigator.pop(context),
            )
          ],
        ),
      );
    });
  }
}
```

[示例代码](https://codepen.io/samlau7245/pen/OJyoovZ)

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(title: "Demo", home: HomePage());
  }
}

class HomePage extends StatefulWidget {
  HomePage({Key key}) : super(key: key);
  @override
  _HomePage createState() => new _HomePage();
}

class _HomePage extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Builder(
        builder: (BuildContext context) => Center(
          child: FlatButton(
            child: Text("Alert"),
            onPressed: () {
              showModalBottomSheet<void>(
                  context: context,
                  backgroundColor: Colors.pink,
                  barrierColor: Colors.red,
                  elevation: 9.0,
                  shape: BeveledRectangleBorder(
                      borderRadius: BorderRadius.circular(12)),
                  clipBehavior: Clip.antiAlias,
                  builder: (_) {
                    return Container(
                      child: const Text('BottomSheet'),
                      height: 400.0,
                    );
                  }).then(
                (value) {},
              );
            },
          ),
        ),
      ),
    );
  }
}
```
<img src="/assets/images/flutter/81.png" width = "25%" height = "25%"/>
