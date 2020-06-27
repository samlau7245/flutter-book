
# [CheckboxListTile(复选框)](https://api.flutter.dev/flutter/material/CheckboxListTile-class.html)

```dart
const CheckboxListTile({
  Key key,
  @required this.value,
  @required this.onChanged,

  this.activeColor,
  this.checkColor,
  
  this.title,
  this.subtitle,
  
  this.isThreeLine = false,
  this.dense,
  this.secondary,// 图标
  this.selected = false,
  this.controlAffinity = ListTileControlAffinity.platform,
  this.autofocus = false,
});
```

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

class CheckboxListTileDemo extends StatefulWidget {
  @override
  _CheckboxListTileDemoState createState() => _CheckboxListTileDemoState();
}

class _CheckboxListTileDemoState extends State<CheckboxListTileDemo> {
  bool _checkboxSelected = false;
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("CheckboxListTile Demo"),
      ),
      body: Center(
        child: CheckboxListTile(
          title: Text('Animate Slowly'),
          value: _checkboxSelected,
          secondary: Icon(Icons.add),
          controlAffinity: ListTileControlAffinity.leading,
          onChanged: (value) {
            setState(() {
              _checkboxSelected = value;
            });
          },
        ),
      ),
    );
  }
}
```

<img src="/assets/images/flutter/86.gif"/>

如果这些样式都满足不了需要，可以使用[Checkbox](https://api.flutter.dev/flutter/material/Checkbox-class.html)和其他的Widgest结合使用。