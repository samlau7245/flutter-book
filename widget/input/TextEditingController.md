
[TextEditingController Class](https://api.flutter.dev/flutter/widgets/TextEditingController-class.html)

# 构造函数

## TextEditingController()

```dart
TextEditingController({
	String text
})
```

## TextEditingController.fromValue()

```dart
TextEditingController.fromValue(
	TextEditingValue value
)
```

# 属性

* `selection` : 当前选中的文本。
* `text` : 当前用户正在输入的文本。
* `value` : 。

# 方法


# 示例

```dart
class _TextFieldExampleState extends State<TextFieldExample> {
  @override
  Widget build(BuildContext context) {
    
    final TextEditingController textEditingController = TextEditingController();
    
    textEditingController.addListener(() {
      print(textEditingController.text);
    });

    return Scaffold(
      appBar: AppBar(
        title: Text("TextFieldExample"),
      ),
      body: Column(
        children: [
          TextField(
            controller: textEditingController,
        ],
      ),
    );
  }
}
```