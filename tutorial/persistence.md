
# 参考资料

* [存储键值对数据](https://flutter.cn/docs/cookbook/persistence/key-value.html)
* [文件读写](https://flutter.cn/docs/cookbook/persistence/reading-writing-files.html)
* [用 SQLite 做数据持久化](https://flutter.cn/docs/cookbook/persistence/sqlite.html)

# 键值对数值存储

对于少量数据可以使用[shared_preferences](https://pub.dev/packages/shared_preferences)进行存储。

# 文件读写

[path_provider](https://pub.flutter-io.cn/packages/path_provider) 提供一种平台无关的方式以一致的方式访问设备的文件位置系统。这个插件只支持iOS、Android。

* 临时文件夹： iOS上是`NSCachesDirectory`，在Android上是`getCacheDir()`。
* `Documents`文件夹： iOS上是`NSDocumentDirectory`，在Android上是`AppData`。

```dart
import 'dart:io';
import 'package:path_provider/path_provider.dart';

// 找到正确的本地路径
Future<String> _localPath() async {
  final dir = await getApplicationDocumentsDirectory();
  return dir.path;
}

// 创建一个指向文件位置的引用
Future<File> _localFile(String file) async {
  final path = await _localPath();
  return File("$path/$file");
}

// 将数据写入文件
Future<File> _writeToPath() async {
  final File file = await _localFile("counter.txt");
  file.writeAsString("StringData");
}

// 从文件读取数据
Future<String> _readFromPath() async {
  try {
    final File file = await _localFile("counter.txt");
    String contents = await file.readAsString();
    print(contents);
    return contents;
  } catch (e) {
    print("error");
    return "";
  }
}
```

# 用 SQLite 做数据持久化

如果是需要存储大量的数据就不推荐使用键值对存储，可以使用[sqflite](https://pub.flutter-io.cn/packages/sqflite)插件，来使用SQLite数据库。

需要的依赖插件:

* [sqflite](https://pub.flutter-io.cn/packages/sqflite) 提供了丰富的类和方法，以便你能便捷实用 SQLite 数据库。
* [path](https://pub.flutter-io.cn/packages/path) 提供了大量方法，以便你能正确的定义数据库在磁盘上的存储位置。

```dart
import 'package:path/path.dart';
import 'package:sqflite/sqflite.dart';

// 打开数据库
Future<Database> _openDataBase() async {
  String dbPath = await getDatabasesPath();
  print(dbPath);
  // 如果本地没有test.db数据库，则会在本地创建一个空的test.db数据库。
  Database database = await openDatabase(
    join(dbPath, "test.db"),
    onCreate: (Database db, int version) {
      // 创建数据表
      return db.execute(
          "CREATE TABLE dogs(id INTEGER PRIMARY KEY, name TEXT, age INTEGER, age1 INTEGER)");
    },
    version: 1,
  );
  return database;
}

// 插入数据
_insertDogField(Dog dog) async {
  Database db = await _openDataBase();
  await db.insert(
    "dogs",
    dog.toMap(),
    conflictAlgorithm: ConflictAlgorithm.replace,
  );
}

_insertDemo() async {
  final fido = Dog(
    id: 0,
    name: 'Fido',
    age: 35,
  );
  await _insertDogField(fido);
}

// 查询数据
_queryDog() async {
  final Database db = await _openDataBase();
  final List<Map<String, dynamic>> list = await db.query('dogs');
  print(list);
}

// 更新数据
Future<void> _updateDog(Dog dog) async {
  final Database db = await _openDataBase();
  await db.update(
    'dogs',
    dog.toMap(),
    where: "id = ?",
    whereArgs: [dog.id],
  );
}

// 删除数据
Future<void> _delDog(int id) async {
  final Database db = await _openDataBase();
  await db.delete("dogs", where: "id = ?", whereArgs: [id]);
}
```

表数据模型

```dart
class Dog {
  final int id;
  final String name;
  final int age;

  Dog({this.id, this.name, this.age});

  Map<String, dynamic> toMap() {
    return {
      'id': id,
      'name': name,
      'age': age,
    };
  }
}
```
























































