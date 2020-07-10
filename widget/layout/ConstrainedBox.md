
* [ConstrainedBox class](https://api.flutter.dev/flutter/widgets/ConstrainedBox-class.html) : 限定子元素child的最大宽度、最大高度、最小宽度和最小高度。例如：通过`ConstrainedBox`来限制文本 Widget 的最大宽度，使其跨越多行。

<iframe width="560" height="315" src="https://www.youtube.com/embed/o2KveVr7adg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 构造函数

```dart
ConstrainedBox({
  Key key,
  @required BoxConstraints constraints,
  Widget child
})
```

# 示例

## BoxConstraints() 

[ConstrainedBoxExample.dart](https://gitee.com/SamLearning/FlutterExample/blob/master/widgets/lib/Layout/ConstrainedBoxExample.dart)

```dart
@override
Widget build(BuildContext context) {
  final String longString =
      "Bacon ipsum dolor amet alcatra spare ribs cow, ribeye fatback tail biltong salami pastrami pork chop bacon sausage tongue turkey.Bacon ipsum dolor amet alcatra spare ribs cow, ribeye fatback tail biltong salami pastrami pork chop bacon sausage tongue turkey. ";
  final String shortString = "Short String!";

  return Scaffold(
    appBar: AppBar(title: Text("ConstrainedBoxExample")),
    body: Column(
      children: [
        ConstrainedBox(
          constraints: BoxConstraints(),
          child: createTextContainer(Colors.red, shortString),
        ),
        ConstrainedBox(
          constraints: BoxConstraints(),
          child: createTextContainer(Colors.green, longString),
        ),
        ConstrainedBox(
          constraints: BoxConstraints(minWidth: 200, minHeight: 150),
          child: createTextContainer(Colors.blue, shortString),
        ),
        ConstrainedBox(
          constraints: BoxConstraints(maxWidth: 200, maxHeight: 150),
          child: createTextContainer(Colors.pink, longString),
        ),
      ],
    ),
  );
}
```

<img src="/assets/images/widgets/05.png"/>

## BoxConstraints.tight()

传一个固定尺寸的 Size。

```dart
@override
Widget build(BuildContext context) {
  final String longString =
      "Bacon ipsum dolor amet alcatra spare ribs cow, ribeye fatback tail biltong salami pastrami pork chop bacon sausage tongue turkey.Bacon ipsum dolor amet alcatra spare ribs cow, ribeye fatback tail biltong salami pastrami pork chop bacon sausage tongue turkey. ";
  final String shortString = "Short String!";

  return Scaffold(
    appBar: AppBar(title: Text("ConstrainedBoxExample")),
    body: Padding(
      padding: const EdgeInsets.all(8.0),
      child: Column(
        children: [
          ConstrainedBox(
            constraints: BoxConstraints.tight(Size(100, 100)),
            child: createTextContainer(Colors.red, shortString),
          ),
          ConstrainedBox(
            constraints: BoxConstraints.tight(Size(100, 100)),
            child: createTextContainer(Colors.green, longString),
          ),
        ],
      ),
    ),
  );
}
```

<img src="/assets/images/widgets/06.png"/>

## BoxConstraints.tightFor()

`BoxConstraints.tightFor()` : 不设置值，默认填充。如果设置宽高，width=maxWidth、height=maxzHeight。

```dart
@override
Widget build(BuildContext context) {
  final String longString =
      "Bacon ipsum dolor amet alcatra spare ribs cow, ribeye fatback tail biltong salami pastrami pork chop bacon sausage tongue turkey.Bacon ipsum dolor amet alcatra spare ribs cow, ribeye fatback tail biltong salami pastrami pork chop bacon sausage tongue turkey. ";
  final String shortString = "Short String!";

  return Scaffold(
    appBar: AppBar(title: Text("ConstrainedBoxExample")),
    body: Column(
      children: [
        ConstrainedBox(
          constraints: BoxConstraints.tightFor(),
          child: createTextContainer(Colors.red, shortString),
        ),
        ConstrainedBox(
          constraints: BoxConstraints.tightFor(),
          child: createTextContainer(Colors.green, longString),
        ),
        ConstrainedBox(
          constraints: BoxConstraints.tightFor(width: 100, height: 100),
          child: createTextContainer(Colors.red, shortString),
        ),
        ConstrainedBox(
          constraints: BoxConstraints.tightFor(width: 100, height: 100),
          child: createTextContainer(Colors.green, longString),
        ),
      ],
    ),
  );
}
```

<img src="/assets/images/widgets/07.png"/>

## BoxConstraints.tightForFinite()

 tightForFinite() 和 tightFor() 类似，在 tightForFinite() 中可以单独设置 width 或 height；宽度固定会自适应高度，高度固定会自适应宽度。

```dart
 @override
Widget build(BuildContext context) {
  final String longString =
      "Bacon ipsum dolor amet alcatra spare ribs cow, ribeye fatback tail biltong salami pastrami pork chop bacon sausage tongue turkey.Bacon ipsum dolor amet alcatra spare ribs cow, ribeye fatback tail biltong salami pastrami pork chop bacon sausage tongue turkey. ";
  final String shortString = "Short String!";

  return Scaffold(
    appBar: AppBar(title: Text("ConstrainedBoxExample")),
    body: Column(
      children: [
        ConstrainedBox(
          constraints: BoxConstraints.tightForFinite(),
          child: createTextContainer(Colors.red, shortString),
        ),
        ConstrainedBox(
          constraints: BoxConstraints.tightForFinite(),
          child: createTextContainer(Colors.green, longString),
        ),
        ConstrainedBox(
          constraints: BoxConstraints.tightForFinite(width: 200),
          child: createTextContainer(Colors.red, shortString),
        ),
        ConstrainedBox(
          constraints: BoxConstraints.tightForFinite(width: 200),
          child: createTextContainer(Colors.green, longString),
        ),
        ConstrainedBox(
          constraints: BoxConstraints.tightForFinite(height: 100),
          child: createTextContainer(Colors.red, shortString),
        ),
        ConstrainedBox(
          constraints: BoxConstraints.tightForFinite(height: 100),
          child: createTextContainer(Colors.green, longString),
        ),
      ],
    ),
  );
}
```

<img src="/assets/images/widgets/08.png"/>

## BoxConstraints.loose()

`loose()`：最小尺寸为`0`，最大尺寸为设置的 Size。

```dart
@override
Widget build(BuildContext context) {
  final String longString =
      "Bacon ipsum dolor amet alcatra spare ribs cow, ribeye fatback tail biltong salami pastrami pork chop bacon sausage tongue turkey.Bacon ipsum dolor amet alcatra spare ribs cow, ribeye fatback tail biltong salami pastrami pork chop bacon sausage tongue turkey. ";
  final String shortString = "Short String!";

  return Scaffold(
    appBar: AppBar(title: Text("ConstrainedBoxExample")),
    body: Column(
      children: [
        ConstrainedBox(
          constraints: BoxConstraints.loose(Size(200, 100)),
          child: createTextContainer(Colors.red, shortString),
        ),
        ConstrainedBox(
          constraints: BoxConstraints.loose(Size(200, 100)),
          child: createTextContainer(Colors.green, longString),
        ),
      ],
    ),
  );
}
```

<img src="/assets/images/widgets/09.png"/>

## BoxConstraints.expand()

`expand()` 方式是填充方式，默认填满父 Widget 。


