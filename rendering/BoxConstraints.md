
* [BoxConstraints Class](https://api.flutter.dev/flutter/rendering/BoxConstraints-class.html)

# 构造函数

```dart
// 用指定的约束大小创建框架大小
const BoxConstraints({
	double minWidth: 0.0,
	double maxWidth: double.infinity,
	double minHeight: 0.0,
	double maxHeight: double.infinity
})

// 创建扩展为填充另一个框约束的框约束
const BoxConstraints.expand({
	double width,
	double height
})

// 创建禁止大小大于给定大小的框约束
BoxConstraints.loose(
	Size size
)

// 仅用指定大小创建框大小
BoxConstraints.tight(
	Size size
)

// 用指定的约束大小创建框大小
const BoxConstraints.tightFor({
	double width,
	double height
})

// 创建需要给定宽度或高度的框约束，除非它们是无限的
const BoxConstraints.tightForFinite({
	double width: double.infinity,
	double height: double.infinity
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