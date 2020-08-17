
[WillPopScope Class](https://api.flutter.dev/flutter/widgets/WillPopScope-class.html)

以下几种情况我们会用到`WillPopScope`：

* 需要询问用户是否退出。(为了避免用户误触返回按钮而导致APP退出，在很多APP中都拦截了用户点击返回键的按钮，然后进行一些防误触判断，比如当用户在某一个时间段内点击两次时，才会认为用户是要退出（而非误触）。)
* App中有多个`Navigator`，想要的是让其中一个`Navigator 退出`，而不是直接让在Widget tree 底层的`Navigator`退出。

# 构造函数

```dart
const WillPopScope({
	Key key,
	@required Widget child,
	@required WillPopCallback onWillPop
})
```

# 示例

```dart
import 'package:flutter/material.dart';

class WillPopScopeExample extends StatefulWidget {
  @override
  _WillPopScopeExampleState createState() => _WillPopScopeExampleState();
}

class _WillPopScopeExampleState extends State<WillPopScopeExample> {
  DateTime _dateTime;
  @override
  Widget build(BuildContext context) {
    return WillPopScope(
      onWillPop: () async {
        if (_dateTime == null ||
            DateTime.now().difference(_dateTime) > Duration(seconds: 1)) {
          _dateTime = DateTime.now();
          return false;
        }
        return true;
      },
      child: Container(
        child: Text('1秒内连续点击两次返回键则退出APP'),
        alignment: Alignment.center,
      ),
    );
  }
}
```