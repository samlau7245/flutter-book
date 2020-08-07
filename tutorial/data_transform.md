
# JSON String 互转

json对象与字符串的转换是使用json.encode和json.decode的，需要导入import 'dart:convert';

# JSON Model 互转

```yml
dependencies:
  json_annotation: ^3.0.1

dev_dependencies:
  build_runner: 1.10.1
  json_serializable: 3.3.0
```

```dart
import 'package:json_annotation/json_annotation.dart';
part 'news.g.dart';

@JsonSerializable()
class News {
  final String firstName;
  final String middleName;
  final String lastName;

  News(this.firstName, this.middleName, this.lastName);
  factory News.fromJson(Map<String, dynamic> json) => _$NewsFromJson(json);
  Map<String, dynamic> toJson() => _$NewsToJson(this);
}
```

在项目的根目录执行:`flutter packages pub run build_runner build`。

更详细的资料可以参考官方[JSON和序列化数据](https://flutter.cn/docs/development/data-and-backend/json)。

[代码自动生成网站](https://caijinglong.github.io/json2dart/index_ch.html)

## json_annotation

### @JsonKey

```dart
@JsonKey(name: 'registration_date_millis')
final int registrationDateMillis; // 就是把字段 registration_date_millis 转成 registrationDateMillis
```