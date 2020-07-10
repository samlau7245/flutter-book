
* [Expanded Class](https://api.flutter.dev/flutter/widgets/Expanded-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/_rnZaagadyo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
const Expanded({
  Key key,
  int flex: 1,
  @required Widget child
})
```

填充 `Row`、`Column`、`Flex`中所有 child 的空间。

# 示例

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
          title: Text('Flutter Demo'),
        ),
        body: Center(
          child: Column(
            children: <Widget>[
              Row(
                children: <Widget>[
                  Container(
                    color: Colors.blue,
                    width: 100.0,
                    height: 100.0,
                    margin: EdgeInsets.all(2.0),
                    child: Center(
                      child: Text('Container'),
                    ),
                  ),
                  Container(
                    color: Colors.blue,
                    width: 100.0,
                    height: 100.0,
                    margin: EdgeInsets.all(2.0),
                    child: Center(
                      child: Text('Container'),
                    ),
                  ),
                ],
              ),
              Row(
                children: <Widget>[
                  Container(
                    color: Colors.blue,
                    width: 100.0,
                    height: 100.0,
                    margin: EdgeInsets.all(2.0),
                    child: Center(
                      child: Text('Container'),
                    ),
                  ),
                  Expanded(
                    child: Container(
                      color: Colors.amber,
                      height: 100.0,
                      child: Center(
                        child: Text('Expanded'),
                      ),
                    ),
                  ),
                  Container(
                    color: Colors.blue,
                    width: 100.0,
                    height: 100.0,
                    margin: EdgeInsets.all(2.0),
                    child: Center(
                      child: Text('Container'),
                    ),
                  ),
                ],
              ),
              Row(
                children: <Widget>[
                  Expanded(
                    flex: 2,
                    child: Container(
                      color: Colors.amber,
                      height: 100.0,
                      child: Center(
                        child: Text(
                          'Expanded \nflex: 2',
                          textAlign: TextAlign.center,
                        ),
                      ),
                    ),
                  ),
                  Container(
                    color: Colors.blue,
                    width: 100.0,
                    height: 100.0,
                    margin: EdgeInsets.all(2.0),
                    child: Center(
                      child: Text('Container'),
                    ),
                  ),
                  Expanded(
                    flex: 1,
                    child: Container(
                      color: Colors.amber,
                      height: 100.0,
                      child: Center(
                        child: Text(
                          'Expanded \nflex: 1',
                          textAlign: TextAlign.center,
                        ),
                      ),
                    ),
                  ),
                ],
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/73.png" width = "25%" height = "25%"/>
