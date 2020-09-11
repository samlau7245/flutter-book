

* [DataTable](https://api.flutter.dev/flutter/material/DataTable-class.html)
* [DataColumn](https://api.flutter.dev/flutter/material/DataColumn-class.html)
* [DataRow](https://api.flutter.dev/flutter/material/DataRow-class.html)
* [DataCell](https://api.flutter.dev/flutter/material/DataCell-class.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/ktTajqbhIcY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



# 构造函数

## DataTable

```dart
DataTable({
  Key key,
  @required List<DataColumn> columns,
  @required List<DataRow> rows

  int sortColumnIndex, 表格显示排序图标的索引
  bool sortAscending: true, 参数表示升序或者降序

  ValueSetter<bool> onSelectAll,
  bool showCheckboxColumn: true,

  double dataRowHeight: kMinInteractiveDimension,
  double headingRowHeight: 56.0,
  double horizontalMargin: 24.0,
  double columnSpacing: 56.0,
  double dividerThickness: 1.0,
})
```

## DataColumn

```dart
DataColumn({
  @required Widget label, 
  String tooltip, 
  bool numeric: false, 默认情况下数据是左对齐的，让某一列右对齐只需设置DataColumn中numeric参数true
  DataColumnSortCallback onSort
})
```

## DataRow

```dart
DataRow({
  LocalKey key, 
  @required List<DataCell> cells

  bool selected: false, 
  ValueChanged<bool> onSelectChanged, 
  MaterialStateProperty<Color> color, 
})

DataRow.byIndex({
  @required List<DataCell> cells

  int index, 
  bool selected: false, 
  ValueChanged<bool> onSelectChanged, 
  MaterialStateProperty<Color> color, 
})
```

## DataCell

```dart
DataCell(Widget child, {
  bool placeholder: false, 
  bool showEditIcon: false, 
  VoidCallback onTap
})
```

# 示例

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text("Demo"),
    ),
    body: DataTable(
      columns: [
        DataColumn(label: Text("Column1")),
        DataColumn(label: Text("Column2")),
      ],
      rows: [
        DataRow(
          selected: true,
          onSelectChanged: (isSelected) {},
          cells: [
            DataCell(
              Container(
                child: Text("Cell1"),
              ),
            ),
            DataCell(
              Container(
                child: Text("Cell2"),
              ),
            ),
          ],
        ),
        DataRow(
          cells: [
            DataCell(
              Container(
                child: Text("Cell1"),
              ),
            ),
            DataCell(
              Container(
                child: Text("Cell2"),
              ),
              showEditIcon: true,
              onTap: () {
                print("object");
              },
            ),
          ],
        ),
      ],
    ),
  );
}
```

<img src="/assets/images/widgets/66.png"/>

## 排序

```dart
DataTable(
  sortAscending: true,
  sortColumnIndex: 0,
  columns: [
    DataColumn(
        label: Text("Column1"),
        onSort: (index, sort) {
          print("$index, $sort");
        }),
    DataColumn(label: Text("Column2")),
  ],
  rows: [
    DataRow(
      cells: [
        DataCell(Container(child: Text("Cell1"))),
        DataCell(Container(child: Text("Cell2"))),
      ],
    ),
    DataRow(
      cells: [
        DataCell(Container(child: Text("Cell1"))),
        DataCell(Container(child: Text("Cell2"))),
      ],
    ),
  ],
)
```

<img src="/assets/images/widgets/67.png"/>

## 列居右

```dart
DataTable(
  columns: [
    DataColumn(label: Text("Column1")),
    DataColumn(label: Text("Column2"), numeric: true),
  ]
  ...
),
```

<img src="/assets/images/widgets/68.png"/>

# 其他

[示例](https://codepen.io/samlau7245/pen/WNQgBQB)

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      home: MainPage(),
    );
  }
}

class MainPage extends StatefulWidget {
  @override
  _MainPage createState() => new _MainPage();
}

class _MainPage extends State<StatefulWidget> {
  List<DataColumn> columnsTitles = List.generate(3, (index) {
    return DataColumn(
      numeric: true,
      label: Text("COL$index", style: TextStyle(fontStyle: FontStyle.italic)),
    );
  });
  List<DataRow> rows = List.generate(20, (index) {
    return DataRow(
      selected: index == 2 ? true : false,
      onSelectChanged: (bool value){
        print('object-$index');
      },
      cells: <DataCell>[
        DataCell(Text('co1-$index'),showEditIcon: true),
        DataCell(Text('co2-$index'),showEditIcon: true),
        DataCell(Text('co3-$index'),showEditIcon: true),
      ],
    );
  });

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Demo"),
      ),
      body: DataTable(
        columns: <DataColumn>[
          DataColumn(
            // numeric: true,
            label: Text(
              "COL1",
              style: TextStyle(fontStyle: FontStyle.italic),
            ),
            tooltip: "Column Tips"
          ),
          DataColumn(
            // numeric: true,
            label: Text(
              "COL22",
              style: TextStyle(fontStyle: FontStyle.italic),
            ),
          ),
          DataColumn(
            numeric: true,
            label: Text(
              "COL3",
              style: TextStyle(fontStyle: FontStyle.italic),
            ),
          ),
        ],
        rows: rows,
      ),
    );
  }
}
```

<img src="/assets/images/flutter/85.png" width = "25%" height = "25%"/>

## [PaginatedDataTable](https://api.flutter.dev/flutter/material/PaginatedDataTable-class.html)

```dart
PaginatedDataTable({
  Key key,
  @required this.header,//表头
  this.actions,
  @required this.columns,
  this.sortColumnIndex,
  this.sortAscending = true,
  this.onSelectAll,
  this.dataRowHeight = kMinInteractiveDimension,
  this.headingRowHeight = 56.0,
  this.horizontalMargin = 24.0,
  this.columnSpacing = 56.0,
  this.showCheckboxColumn = true,
  this.initialFirstRowIndex = 0,
  this.onPageChanged,
  this.rowsPerPage = defaultRowsPerPage,
  this.availableRowsPerPage = const <int>[defaultRowsPerPage, defaultRowsPerPage * 2, defaultRowsPerPage * 5, defaultRowsPerPage * 10],
  this.onRowsPerPageChanged,
  this.dragStartBehavior = DragStartBehavior.start,
  @required this.source,
});
```

# Table

* [Table (Flutter Widget of the Week)](https://www.youtube.com/watch?v=_lbE0wsVZSw)
* [Table Class](https://api.flutter.dev/flutter/widgets/Table-class.html)

## DataTable 

* [DataTable (Flutter Widget of the Week)](https://www.youtube.com/watch?v=ktTajqbhIcY)
* [CodePen-DataTable,搭配视频讲解看](https://codepen.io/samlau7245/pen/pojVMdj)

## SingleChildScrollView
* [SingleChildScrollView-DataTable](https://codepen.io/samlau7245/pen/oNjdKqd)

## [PaginatedDataTable]()