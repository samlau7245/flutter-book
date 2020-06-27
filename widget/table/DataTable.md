
# [DataTable](https://api.flutter.dev/flutter/material/DataTable-class.html)

* [DataColumn](https://api.flutter.dev/flutter/material/DataColumn-class.html)
* [DataRow](https://api.flutter.dev/flutter/material/DataRow-class.html)

```dart
DataTable({
  Key key,
  @required this.columns,
  this.sortColumnIndex,
  this.sortAscending = true,
  this.onSelectAll,
  this.dataRowHeight = kMinInteractiveDimension,
  this.headingRowHeight = 56.0,
  this.horizontalMargin = 24.0,
  this.columnSpacing = 56.0,
  this.showCheckboxColumn = true,
  this.dividerThickness = 1.0,
  @required this.rows,
});

const DataColumn({
  @required this.label,
  this.tooltip,
  this.numeric = false,
  this.onSort,
});

const DataRow({
  this.key,
  this.selected = false,
  this.onSelectChanged,
  @required this.cells,
});

const DataCell(
  this.child, {
  this.placeholder = false,//显示缺省
  this.showEditIcon = false,// 显示编辑按钮
  this.onTap,
});

```

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