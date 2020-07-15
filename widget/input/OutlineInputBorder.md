
[OutlineInputBorder Class](https://api.flutter.dev/flutter/material/OutlineInputBorder/OutlineInputBorder.html)

# 构造函数

```dart
const OutlineInputBorder({
	BorderSide borderSide: const BorderSide(),
	BorderRadius borderRadius: const BorderRadius.all(Radius.circular(4.0)),
	double gapPadding: 4.0
})
```

# 示例

```dart
TextField(
  controller: textEditingController,
  decoration: InputDecoration(
    labelText: 'Hello',
    prefixIcon: Icon(Icons.phone),
    suffixIcon: Icon(Icons.offline_bolt),
    border: OutlineInputBorder(
      borderRadius: BorderRadius.circular(15.0),
    ),
  ),
)
```

<img src="/assets/images/widgets/24.png"/>