
* [TableRow](https://api.flutter.dev/flutter/material/TableRow-class.html)
* [TableColumnWidth](https://api.flutter.dev/flutter/material/TableColumnWidth-class.html)
	* [FixedColumnWidth](https://api.flutter.dev/flutter/rendering/FixedColumnWidth-class.html)
	* [FlexColumnWidth](https://api.flutter.dev/flutter/rendering/FlexColumnWidth-class.html)
	* [FractionColumnWidth](https://api.flutter.dev/flutter/rendering/FractionColumnWidth-class.html)
	* [IntrinsicColumnWidth](https://api.flutter.dev/flutter/rendering/IntrinsicColumnWidth-class.html)
	* [MaxColumnWidth](https://api.flutter.dev/flutter/rendering/MaxColumnWidth-class.html)
	* [MinColumnWidth](https://api.flutter.dev/flutter/rendering/MinColumnWidth-class.html)
* [TableBorder](https://api.flutter.dev/flutter/material/TableBorder-class.html)
* [TableCellVerticalAlignment](https://api.flutter.dev/flutter/rendering/TableCellVerticalAlignment-class.html)
* [TableCell](https://api.flutter.dev/flutter/widgets/TableCell-class.html)
* [TableRowInkWell](https://api.flutter.dev/flutter/material/TableRowInkWell-class.html)

# 构造函数

## Table

```dart
Table({
	Key key,
	List<TableRow> children: const [],
	Map<int, TableColumnWidth> columnWidths,
	TableColumnWidth defaultColumnWidth: const FlexColumnWidth(1.0),
	TextDirection textDirection,
	TableBorder border,
	TableCellVerticalAlignment defaultVerticalAlignment: TableCellVerticalAlignment.top,
	TextBaseline textBaseline: TextBaseline.alphabetic
})
```

## TableRow

```dart
TableRow({LocalKey key, 
	Decoration decoration, 
	List<Widget> children
})
```

## TableBorder

```dart
TableBorder({
	BorderSide top: BorderSide.none, 
	BorderSide right: BorderSide.none, 
	BorderSide bottom: BorderSide.none, 
	BorderSide left: BorderSide.none, 
	BorderSide horizontalInside: BorderSide.none, 
	BorderSide verticalInside: BorderSide.none
})

TableBorder.all({
	Color color: const Color(0xFF000000), 
	double width: 1.0, 
	BorderStyle style: BorderStyle.solid
})

TableBorder.symmetric({
	BorderSide inside: BorderSide.none, 
	BorderSide outside: BorderSide.none
})
```

## TableCell

```dart
TableCell({
	Key key, 
	TableCellVerticalAlignment verticalAlignment, 
	@required Widget child
})
```

## TableColumnWidth

```dart
TableColumnWidth()

FixedColumnWidth(double value)

FlexColumnWidth([double value = 1.0])

FractionColumnWidth(double value)

IntrinsicColumnWidth({double flex})

MaxColumnWidth(TableColumnWidth a, TableColumnWidth b)

MinColumnWidth(TableColumnWidth a, TableColumnWidth b)
```

# 示例

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text("刷新"),
    ),
    body: Table(
      border: new TableBorder.all(width: 1.0, color: Colors.purpleAccent),
      children: [
        TableRow(
          children: [
            TableCell(child: Center(child: Text("data1"))),
            TableCell(child: Center(child: Text("data1"))),
            TableCell(child: Center(child: Text("data1"))),
          ],
        ),
        TableRow(
          children: [
            TableCell(child: Center(child: Text("data1"))),
            TableCell(child: Center(child: Text("data1"))),
            TableCell(child: Center(child: Text("data1"))),
          ],
        ),
      ],
    ),
  );
}
```

<img src="/assets/images/widgets/65.png"/>
