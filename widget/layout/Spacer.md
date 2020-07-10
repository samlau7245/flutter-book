
* [Spacer Class](https://api.flutter.dev/flutter/widgets/Spacer-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/7FJgd7QN1zI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
const Spacer({
	Key key,
	int flex: 1
})
```

Creates a flexible space to insert into a `Flexible` widget.

# 示例

```dart
class _SpacerExampleState extends State<SpacerExample> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("FlexibleExample"),
      ),
      body: Row(
        children: [
          Container(color: Colors.red, width: 80, height: 80),
          Spacer(flex: 1),
          Container(color: Colors.green, width: 80, height: 80),
          Spacer(flex: 5),
          Container(color: Colors.blue, width: 80, height: 80),
        ],
      ),
    );
  }
}
```

<img src="/assets/images/widgets/11.png"/>