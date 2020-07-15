
[DropdownButton Class](https://api.flutter.dev/flutter/material/DropdownButton-class.html)

# 构造函数

## DropdownButton 

```dart
DropdownButton<T>({
	Key key,
	@required List<DropdownMenuItem<T>> items,
	DropdownButtonBuilder selectedItemBuilder,
	T value, // 当前选定的值，如果没有选择任何一个，则为空。
	Widget hint,
	Widget disabledHint, // 禁用下拉列表的时候显示的消息。
	@required ValueChanged<T> onChanged, // 当用户选择了其中一个值得时候触发
	VoidCallback onTap,
	int elevation: 8, // 菜单展开时的阴影
	TextStyle style,
	Widget underline, // 绘制按钮下划线
	Widget icon, // 下拉指示图标
	Color iconDisabledColor,
	Color iconEnabledColor,
	double iconSize: 24.0,
	bool isDense: false,
	bool isExpanded: false, // 是否填充
	double itemHeight: kMinInteractiveDimension,
	Color focusColor,
	FocusNode focusNode,
	bool autofocus: false,
	Color dropdownColor
})
```

## DropdownMenuItem 

`DropdownButton`中的item。

```dart
const DropdownMenuItem<T>({
	Key key,
	VoidCallback onTap,
	T value,
	@required Widget child
})
```

# 示例

```dart
class _DropdownButtonExampleState extends State<DropdownButtonExample> {
  String selectedValue = '';
  List dropdownList = ['One', 'Two', 'Three', 'Four'];

  @override
  void initState() {
    selectedValue = dropdownList.first;
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("DropdownButtonExample"),
      ),
      body: DropdownButton(
        isExpanded: true,
        icon: Icon(Icons.arrow_downward),
        value: selectedValue,
        items: dropdownList
            .map((e) => DropdownMenuItem(
                  child: Text(e),
                  value: e,
                ))
            .toList(),
        onChanged: (newValue) {
          setState(() {
            print(newValue);
            selectedValue = newValue;
          });
        },
      ),
    );
  }
}
```

<img src="/assets/images/widgets/26.png"/>

设置菜单的阴影值：

```dart
elevation: 24,
```
<img src="/assets/images/widgets/27.png"/>