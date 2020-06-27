# [ExpansionPanel](https://api.flutter.dev/flutter/material/ExpansionPanel-class.html)

```dart
class ExpansionPanel{}

class ExpansionPanelList extends StatefulWidget{
  const ExpansionPanelList({
    Key key,
    this.children = const <ExpansionPanel>[],
    this.expansionCallback,
    this.animationDuration = kThemeAnimationDuration,
    this.expandedHeaderPadding = _kPanelHeaderExpandedDefaultPadding,
  });
}

class ExpansionPanelRadio extends ExpansionPanel{}
```

## [ExpansionPanelList](https://api.flutter.dev/flutter/material/ExpansionPanelList-class.html)

[示例](https://codepen.io/samlau7245/pen/rNOZqOL)

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(title: "Demo", home: HomePage());
  }
}

// 数据模型
class Item {
  Item({this.expandedValue, this.headerValue, this.isExpanded = false});

  String expandedValue;
  String headerValue;
  bool isExpanded;
}

List<Item> generateItems(int length) {
  return List.generate(
    length,
    (index) => Item(
        headerValue: 'Panel $index',
        expandedValue: 'This is item number $index'),
  );
}

class HomePage extends StatefulWidget {
  HomePage({Key key}) : super(key: key);
  @override
  _HomePage createState() => new _HomePage();
}

class _HomePage extends State<HomePage> {
  List<Item> list = generateItems(8);
  Widget _buildPanel() {
    return ExpansionPanelList(
      children: list.map<ExpansionPanel>((Item item) {
        return ExpansionPanel(
          headerBuilder: (BuildContext context, bool isExpanded) {
            return ListTile(title: Text(item.headerValue));
          },
          body: ListTile(
            title: Text(item.expandedValue),
            subtitle: Text('To delete this panel, tap the trash can icon'),
            trailing: Icon(Icons.delete),
            onTap: () {},
          ),
          isExpanded: item.isExpanded,
        );
      }).toList(),
      expansionCallback: (int index, bool isExpanded) {
        setState(() {
          list[index].isExpanded = !isExpanded;
        });
      },
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SingleChildScrollView(
        child: Container(
          child: _buildPanel(),
        ),
      ),
    );
  }
}
```

## [ExpansionPanelList.radio](https://api.flutter.dev/flutter/material/ExpansionPanelList/ExpansionPanelList.radio.html)

[CodePen-ExpansionPanelList.radio](https://codepen.io/samlau7245/pen/VwvGEKX)

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(title: "Demo", home: HomePage());
  }
}

// 数据模型
class Item {
  Item({this.expandedValue, this.headerValue, this.id});

  String expandedValue;
  String headerValue;
  int id;
}

List<Item> generateItems(int length) {
  return List.generate(
    length,
    (index) => Item(
        id: index,
        headerValue: 'Panel $index',
        expandedValue: 'This is item number $index'),
  );
}

class HomePage extends StatefulWidget {
  HomePage({Key key}) : super(key: key);
  @override
  _HomePage createState() => new _HomePage();
}

class _HomePage extends State<HomePage> {
  List<Item> list = generateItems(8);
  Widget _buildPanel() {
    return ExpansionPanelList.radio(
      initialOpenPanelValue: 2,
      children: list.map<ExpansionPanelRadio>((Item item) {
        return ExpansionPanelRadio(
          headerBuilder: (BuildContext context, bool isExpanded) {
            return ListTile(title: Text(item.headerValue));
          },
          body: ListTile(
            title: Text(item.expandedValue),
            subtitle: Text('To delete this panel, tap the trash can icon'),
            trailing: Icon(Icons.delete),
            onTap: () {},
          ),
          value: item.id,
        );
      }).toList(),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SingleChildScrollView(
        child: Container(
          child: _buildPanel(),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/82.gif"/>