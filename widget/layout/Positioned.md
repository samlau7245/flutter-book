
[Positioned Class](https://api.flutter.dev/flutter/widgets/Positioned-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/EgtPleVwxBQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
const Positioned({
	Key key, 
	double left, 
	double top, 
	double right, 
	double bottom, 
	double width, 
	double height, 
	@required Widget child
})

factory Positioned.directional({
	Key key, 
	@required TextDirection textDirection, 
	double start, 
	double top, 
	double end, 
	double bottom, 
	double width, 
	double height, 
	@required Widget child
})

const Positioned.fill({
	Key key, 
	double left: 0.0, 
	double top: 0.0, 
	double right: 0.0, 
	double bottom: 0.0, 
	@required Widget child
})

const Positioned.fromRect({
	Key key, 
	Rect rect, 
	@required Widget child
})

const Positioned.fromRelativeRect({
	Key key, 
	RelativeRect rect, 
	@required Widget child
})
```

> `Positioned`需要在`Stack`中使用。

# 示例

```dart
class _PositionedExampleState extends State<PositionedExample> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text("PositionedExample"),
        ),
        body: Stack(
          children: [
            Positioned(
              top: 50,
              child: Container(
                child: Text("red"),
                color: Colors.red,
                padding: EdgeInsets.all(10.0),
              ),
            ),
            Positioned(
              top: 100,
              left: 100,
              child: Container(
                child: Text("green"),
                color: Colors.green,
                padding: EdgeInsets.all(10.0),
              ),
            ),
            Positioned(
              top: 150,
              left: 150,
              child: Container(
                child: Text("blue"),
                color: Colors.blue,
                padding: EdgeInsets.all(10.0),
              ),
            )
          ],
        ));
  }
}
```

<img src="/assets/images/widgets/13.png"/>
