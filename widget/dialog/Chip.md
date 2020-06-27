
# [Chip](https://api.flutter.dev/flutter/material/Chip-class.html)

* [InputChip](https://api.flutter.dev/flutter/material/InputChip-class.html)
* [ChoiceChip](https://api.flutter.dev/flutter/material/ChoiceChip-class.html)
* [FilterChip](https://api.flutter.dev/flutter/material/FilterChip-class.html)
* [ActionChip](https://api.flutter.dev/flutter/material/ActionChip-class.html)
* [查看官方测试文件](https://github.com/flutter/flutter/blob/5d5175b0b3d044574eec48a8b9b17095f58fd576/packages/flutter/test/material/chip_test.dart)

<img src="/assets/images/flutter/84.png"/>

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(title: "Demo", home: HomePage());
  }
}

class ActorFilterEntry {
  const ActorFilterEntry(this.name, this.initials);
  final String name;
  final String initials;
}

class HomePage extends StatefulWidget {
  HomePage({Key key}) : super(key: key);
  @override
  _HomePage createState() => new _HomePage();
}

class _HomePage extends State<HomePage> {
  ///////////////////////////////////////////////
  Chip _chip() {
    return Chip(
      avatar: CircleAvatar(
        backgroundColor: Colors.grey.shade800,
        child: Text('AB'),
      ),
      deleteButtonTooltipMessage: 'Delete chip A',
      label: Text('Aaron Burr'),
      onDeleted: () {
        print('Chip.');
      },
    );
  }

  ///////////////////////////////////////////////

  bool _inputChipSlected = false;
  InputChip _inputChip() {
    return InputChip(
      avatar: CircleAvatar(
        backgroundColor: Colors.grey.shade800,
        child: Text('AB'),
      ),
      label: Text('Aaron Burr'),
      selected: _inputChipSlected,
      onSelected: (bool value) {
        setState(() {
          _inputChipSlected = value;
        });
      },
    );
  }

  ///////////////////////////////////////////////

  int _value = 1;
  Wrap _choiceChip() {
    return Wrap(
      children: List<Widget>.generate(
        3,
        (int index) {
          return ChoiceChip(
            label: Text('Item $index'),
            selected: _value == index,
            onSelected: (bool selected) {
              setState(() {
                _value = selected ? index : null;
              });
            },
          );
        },
      ).toList(),
    );
  }

  ///////////////////////////////////////////////
  final List<ActorFilterEntry> _cast = <ActorFilterEntry>[
    const ActorFilterEntry('Aaron Burr', 'AB'),
    const ActorFilterEntry('Alexander Hamilton', 'AH'),
    const ActorFilterEntry('Eliza Hamilton', 'EH'),
    const ActorFilterEntry('James Madison', 'JM'),
  ];
  List<String> _filters = <String>[];
  Iterable<Widget> get actorWidgets sync* {
    for (final ActorFilterEntry actor in _cast) {
      yield Padding(
        padding: const EdgeInsets.all(4.0),
        child: FilterChip(
          avatar: CircleAvatar(child: Text(actor.initials)),
          label: Text(actor.name),
          selected: _filters.contains(actor.name),
          onSelected: (bool value) {
            setState(() {
              if (value) {
                _filters.add(actor.name);
              } else {
                _filters.removeWhere((String name) {
                  return name == actor.name;
                });
              }
            });
          },
        ),
      );
    }
  }

  ///////////////////////////////////////////////
  ActionChip _actionChip() {
    return ActionChip(
        avatar: CircleAvatar(
          backgroundColor: Colors.grey.shade800,
          child: Text('AB'),
        ),
        label: Text('Aaron Burr'),
        onPressed: () {
          print("If you stand for nothing, Burr, what’ll you fall for?");
        });
  }

  ///////////////////////////////////////////////

  Container demo1() {
    return Container(
      width: 75.0,
      height: 25.0,
      child: Chip(
        label: Container(
          width: 100.0,
          height: 50.0,
        ),
        onDeleted: () {},
      ),
    );
  }

  InputChip demo2() {
    return InputChip(
      label: const Text('InputChip'),
      selected: true,
      showCheckmark: true,
      checkmarkColor: Colors.red,
    );
  }

  Widget _selectedFilterChip({Color checkmarkColor}) {
    return FilterChip(
      label: const Text('InputChip'),
      selected: true,
      showCheckmark: true,
      checkmarkColor: checkmarkColor,
      onSelected: (bool _) {},
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: <Widget>[
          _chip(),
          _inputChip(),
          _choiceChip(),
          Wrap(children: actorWidgets.toList()),
          _actionChip(),
          demo1(),
          demo2(),
          _selectedFilterChip(checkmarkColor: Colors.red),
        ],
      ),
    );
  }
}
```