
# Expanded(填充布局)

* [Expanded (Flutter Widget of the Week)](https://www.youtube.com/watch?v=_rnZaagadyo)
* [Expanded Class](https://api.flutter.dev/flutter/widgets/Expanded-class.html)

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
