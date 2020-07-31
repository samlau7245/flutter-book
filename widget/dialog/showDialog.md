
[showDialog](https://api.flutter.dev/flutter/material/showDialog.html)

# 构造函数

```dart
Future<T> showDialog <T>({
	@required BuildContext context,
	bool barrierDismissible: true,
	Widget child,
	WidgetBuilder builder,
	bool useRootNavigator: true,
	RouteSettings routeSettings
})
```

# 示例

```dart
Future<void> _showMyDialog() async {
  return showDialog<void>(
    context: context,
    barrierDismissible: false, // user must tap button!
    builder: (BuildContext context) {
      return AlertDialog(
        title: Text('AlertDialog Title'),
        content: SingleChildScrollView(
          child: ListBody(
            children: <Widget>[
              Text('This is a demo alert dialog.'),
              Text('Would you like to approve of this message?'),
            ],
          ),
        ),
        actions: <Widget>[
          FlatButton(
            child: Text('Approve'),
            onPressed: () {
              Navigator.of(context).pop();
            },
          ),
        ],
      );
    },
  );
}
```

## 控制弹窗的Size

```dart
Future<void> _showDialog() async {
  return showDialog(
    context: context,
    builder: (_) {
      return Center( // 如果没有center()，会全屏展示，就算Container()设置了尺寸也没用。Flutter needs a way to know how to align that 200x150 box inside the screen.
        child: Container(
          height: 200,
          width: 150,
          color: Colors.red,
        ),
      );
    },
  );
}
```

<img src="/assets/images/widgets/31.png"/>
