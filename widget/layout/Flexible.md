
* [Flexible Class](https://api.flutter.dev/flutter/widgets/Flexible-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/CI7x0mAZiY0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
const Flexible({
	Key key,
	int flex: 1,
	FlexFit fit: FlexFit.loose,
	@required Widget child
})

enum FlexFit {
  tight, // 会尽可能的占用空间
  loose, // 则按照子控件的自身尺寸的需要
}
```

当 FlexFit 设置 `fit:FlexFit.tight`，效果相当于`Expanded`。

# Flexible VS Expanded

* `...` -> `Flexible`
* `...` -> `Flexible` -> `Expanded`

`Expanded`是继承自`Flexible`。

* 相同点 : 都必须使用在`Row`、`Column`、`Flex`其中，都可用来配置子布局的比例（权重）适配。
* 不同点 : `Expanded`会强制填充剩余留白空间，而`Flexible`不会强制填充。

```
class _SpacerExampleState extends State<SpacerExample> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("FlexibleExample"),
      ),
      body: Column(
        children: [
          Row(
            children: [
              Container(
                padding: EdgeInsets.all(10),
                decoration: BoxDecoration(color: Colors.red),
                child: Text("short string"),
              ),
              Flexible(
                child: Container(
                  padding: EdgeInsets.all(10),
                  decoration: BoxDecoration(color: Colors.green),
                  child: Text("Flexible "),
                ),
              )
            ],
          ),
          Row(
            children: [
              Container(
                padding: EdgeInsets.all(10),
                decoration: BoxDecoration(color: Colors.blue),
                child: Text("short string"),
              ),
              Expanded(
                child: Container(
                  padding: EdgeInsets.all(10),
                  decoration: BoxDecoration(color: Colors.green),
                  child: Text("Expanded "),
                ),
              )
            ],
          )
        ],
      ),
    );
  }
}
```

<img src="/assets/images/widgets/12.png"/>

# 示例

```dart
class _FlexibleExampleState extends State<FlexibleExample> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("FlexibleExample"),
      ),
      body: Column(
        children: [
          Flexible(flex: 3, child: Container(color: Colors.red)),
          Flexible(flex: 2, child: Container(color: Colors.green)),
          Flexible(flex: 1, child: Container(color: Colors.blue)),
        ],
      ),
    );
  }
}
```

<img src="/assets/images/widgets/10.png"/>
