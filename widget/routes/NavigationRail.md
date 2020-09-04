
* [Material Design](https://material.io/components/navigation-rail)
* [NavigationRail class](https://api.flutter.dev/flutter/material/NavigationRail-class.html)

# 构造函数

```dart
const NavigationRail({
	Color backgroundColor,
	bool extended: false,
	Widget leading,
	Widget trailing,
	@required List<NavigationRailDestination> destinations,
	@required int selectedIndex,
	ValueChanged<int> onDestinationSelected,
	double elevation,
	double groupAlignment,
	NavigationRailLabelType labelType,
	TextStyle unselectedLabelTextStyle,
	TextStyle selectedLabelTextStyle,
	IconThemeData unselectedIconTheme,
	IconThemeData selectedIconTheme,
	double minWidth,
	double minExtendedWidth
});

enum NavigationRailLabelType {
  none, // 仅仅展示 destinations
  selected, // 展示选中 destinations 的 label
  all, // 所有的 destinations 都显示其 label
}
```

# 示例

<img src="/assets/images/widgets/02.png"/>

[NavigationRailExample.dart](https://gitee.com/SamLearning/FlutterExample/blob/master/widgets/lib/class/NavigationRailExample.dart)

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

class NavigationRailExample extends StatefulWidget {
  final String title;
  const NavigationRailExample({Key key, this.title}) : super(key: key);
  @override
  _NavigationRailExampleState createState() => _NavigationRailExampleState();
}

class _NavigationRailExampleState extends State<NavigationRailExample> {
  int _selectedIndex = 0;
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Row(
        children: [
          NavigationRail(
            labelType: NavigationRailLabelType.selected,
            leading: FlatButton(onPressed: () {}, child: Text("Leading")),
            trailing: FlatButton(onPressed: () {}, child: Text("Trailing")),
            destinations: [
              NavigationRailDestination(
                icon: Icon(Icons.favorite_border),
                selectedIcon: Icon(Icons.favorite),
                label: Text('first'),
              ),
              NavigationRailDestination(
                icon: Icon(Icons.bookmark_border),
                selectedIcon: Icon(Icons.book),
                label: Text('Second'),
              ),
              NavigationRailDestination(
                icon: Icon(Icons.star_border),
                selectedIcon: Icon(Icons.star),
                label: Text('Third'),
              )
            ],
            selectedIndex: _selectedIndex,
            onDestinationSelected: (int index) {
              setState(() {
                _selectedIndex = index;
              });
            },
          ),
          VerticalDivider(thickness: 1, width: 1),
          Expanded(
              child: Center(
            child: Text('selectedIndex: $_selectedIndex'),
          ))
        ],
      ),
    );
  }
}
```
