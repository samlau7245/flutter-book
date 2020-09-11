
* [SliverPadding-class](https://api.flutter.dev/flutter/widgets/SliverPadding-class.html)
* [SliverOffstage-class](https://api.flutter.dev/flutter/widgets/SliverOffstage-class.html)
* [SliverOpacity-class](https://api.flutter.dev/flutter/widgets/SliverOpacity-class.html)

# SliverPadding

## 构造函数

`SliverPadding`搭配`CustomScrollView`使用，设置`sliver`的内边距。

```dart
SliverPadding({
	Key key, 
	@required EdgeInsetsGeometry padding, 
	Widget sliver
})
```

## 示例

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: CustomScrollView(
      slivers: [
        SliverAppBar(
          expandedHeight: 250,
          elevation: 0.0,
          flexibleSpace: FlexibleSpaceBar(
            background: Image.network(
              'http://img1.mukewang.com/5c18cf540001ac8206000338.jpg',
              fit: BoxFit.cover,
            ),
          ),
        ),
        SliverPadding(
          padding: EdgeInsets.all(15),
          sliver: SliverList(
            delegate: SliverChildBuilderDelegate(
              (_, index) {
                return Container(
                  height: 100.0,
                  color: Colors.primaries[index % Colors.primaries.length],
                  child: Center(
                    child: Text("$index"),
                  ),
                );
              },
              childCount: 20,
            ),
          ),
        ),
      ],
    ),
  );
}
```

<img src="/assets/images/widgets/57.gif"/>


# SliverOffstage

## 构造函数

`SliverOffstage`搭配`CustomScrollView`使用，设置`sliver`的显示或隐藏。

```dart
SliverOffstage({
	Key key, 
	bool offstage: true,
	Widget sliver
})
```

## 示例

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    floatingActionButton: FloatingActionButton(
      onPressed: () {
        setState(() {
          _title = _offstage ? "隐藏" : "显示";
          _offstage = !_offstage;
        });
      },
      child: Text(_title),
    ),
    body: CustomScrollView(
      slivers: [
        SliverAppBar(
          expandedHeight: 250,
          elevation: 0.0,
          flexibleSpace: FlexibleSpaceBar(
            background: Image.network(
              'http://img1.mukewang.com/5c18cf540001ac8206000338.jpg',
              fit: BoxFit.cover,
            ),
          ),
        ),
        SliverOffstage(
          offstage: _offstage,
          sliver: SliverList(
            delegate: SliverChildBuilderDelegate(
              (_, index) {
                return Container(
                  height: 100.0,
                  color: Colors.primaries[index % Colors.primaries.length],
                  child: Center(
                    child: Text("$index"),
                  ),
                );
              },
              childCount: 20,
            ),
          ),
        ),
      ],
    ),
  );
}
```

<img src="/assets/images/widgets/58.gif"/>

# SliverOpacity

## 构造函数

`SliverOpacity`搭配`CustomScrollView`使用，设置`sliver`的透明度。

```dart
SliverOpacity({
	Key key, 
	@required double opacity, 
	bool alwaysIncludeSemantics: false, 
	Widget sliver
})
```

## 示例

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    floatingActionButton: FloatingActionButton(
      onPressed: () {
        if (_opacity > 0.1) {
          setState(() {
            _opacity = _opacity - 0.1;
          });
        }
      },
      child: Text(_title),
    ),
    body: CustomScrollView(
      slivers: [
        SliverAppBar(
          expandedHeight: 250,
          elevation: 0.0,
          flexibleSpace: FlexibleSpaceBar(
            background: Image.network(
              'http://img1.mukewang.com/5c18cf540001ac8206000338.jpg',
              fit: BoxFit.cover,
            ),
          ),
        ),
        SliverOpacity(
          opacity: _opacity,
          sliver: SliverList(
            delegate: SliverChildBuilderDelegate(
              (_, index) {
                return Container(
                  height: 100.0,
                  color: Colors.primaries[index % Colors.primaries.length],
                  child: Center(
                    child: Text("$index"),
                  ),
                );
              },
              childCount: 20,
            ),
          ),
        ),
      ],
    ),
  );
}
```

<img src="/assets/images/widgets/59.gif"/>

