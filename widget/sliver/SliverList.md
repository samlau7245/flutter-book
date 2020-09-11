
* [SliverList-class](https://api.flutter.dev/flutter/widgets/SliverList-class.html)
* [SliverFixedExtentList-class](https://api.flutter.dev/flutter/widgets/SliverFixedExtentList-class.html)
* [SliverPrototypeExtentList-class](https://api.flutter.dev/flutter/widgets/SliverPrototypeExtentList-class.html)

# 构造函数

```dart
SliverList({
  Key key, 
  @required SliverChildDelegate delegate
})

SliverFixedExtentList({
  Key key, 
  @required SliverChildDelegate delegate, 
  @required double itemExtent
})

SliverPrototypeExtentList({
  Key key, 
  @required SliverChildDelegate delegate, 
  @required Widget prototypeItem
})
```

* `SliverList`通过计算子控件布局去控制自身高度。
* `SliverPrototypeExtentList`的高度是由`prototypeItem`的高度决定的，除此之外用法和`SliverList`一样。
* `SliverFixedExtentList`是固定子控件高度。
* 效率: `SliverPrototypeExtentList` > `SliverFixedExtentList` > `SliverList`。

# 示例

## SliverList、SliverGrid搭配使用

```dart
@override
Widget build(BuildContext context) {
  return CustomScrollView(
    slivers: [
      SliverAppBar(
        title: Text("SliverAppBar"),
        leading: IconButton(
          icon: Icon(Icons.arrow_back),
          onPressed: () {},
        ),
        expandedHeight: 150,
      ),
      SliverGrid(
        delegate: SliverChildBuilderDelegate(
          (_, index) {
            return Container(
              color: Colors.primaries[index % Colors.primaries.length],
              child: Center(
                child: Text("$index"),
              ),
            );
          },
          childCount: 10,
        ),
        gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: 5,
        ),
      ),
      SliverList(
        delegate: SliverChildBuilderDelegate(
          (_, index) {
            return Container(
              height: 50.0,
              color: Colors.primaries[index % Colors.primaries.length],
              child: Center(
                child: Text("$index"),
              ),
            );
          },
          childCount: 10,
        ),
      ),
    ],
  );
}
```

<img src="/assets/images/widgets/52.gif"/>

## SliverFixedExtentList、SliverGrid搭配使用

```dart
@override
Widget build(BuildContext context) {
  return CustomScrollView(
    slivers: [
      SliverAppBar(
        title: Text("SliverAppBar"),
        leading: IconButton(
          icon: Icon(Icons.arrow_back),
          onPressed: () {},
        ),
        expandedHeight: 150,
      ),
      SliverGrid(
        delegate: SliverChildBuilderDelegate(
          (_, index) {
            return Container(
              color: Colors.primaries[index % Colors.primaries.length],
              child: Center(
                child: Text("$index"),
              ),
            );
          },
          childCount: 10,
        ),
        gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: 5,
        ),
      ),
      SliverFixedExtentList(
        delegate: SliverChildBuilderDelegate(
          (_, index) {
            return Container(
              color: Colors.primaries[index % Colors.primaries.length],
              child: Center(
                child: Text("$index"),
              ),
            );
          },
          childCount: 10,
        ),
        itemExtent: 50.0,
      )
    ],
  );
}
```

## SliverPrototypeExtentList、SliverGrid搭配使用

```dart
@override
Widget build(BuildContext context) {
  return CustomScrollView(
    slivers: [
      SliverAppBar(
        title: Text("SliverAppBar"),
        leading: IconButton(
          icon: Icon(Icons.arrow_back),
          onPressed: () {},
        ),
        expandedHeight: 150,
      ),
      SliverGrid(
        delegate: SliverChildBuilderDelegate(
          (_, index) {
            return Container(
              color: Colors.primaries[index % Colors.primaries.length],
              child: Center(
                child: Text("$index"),
              ),
            );
          },
          childCount: 10,
        ),
        gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: 5,
        ),
      ),
      SliverPrototypeExtentList(
        delegate: SliverChildBuilderDelegate(
          (_, index) {
            return Container(
              color: Colors.primaries[index % Colors.primaries.length],
            );
          },
          childCount: 10,
        ),
        prototypeItem: Text(
          '测试',
          style: TextStyle(fontSize: 38),
        ),
      ),
    ],
  );
}
```