[JSON和序列化](https://flutterchina.club/json/)

# 使用 json_serializable 实现

* [便捷工具:JSON转 annotation Model](https://caijinglong.github.io/json2dart/index_ch.html)

## 依赖

涉及三个包：[json_annotation](https://pub.dev/packages/json_annotation)、[build_runner](https://pub.dev/packages/build_runner)、[json_serializable](https://pub.dev/packages/json_serializable)

```yaml
dependencies:
  json_annotation: ^4.0.1

dev_dependencies:
  build_runner: ^2.0.4
  json_serializable: ^4.1.3
```

## 实现

```dart
import 'package:json_annotation/json_annotation.dart';
part 'user.g.dart';

@JsonSerializable()
class User {
  final String name;
  final String age;
  final Grade grade;

  User(this.name, this.age, this.grade);

  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  Map<String, dynamic> toJson() => _$UserToJson(this);
}

@JsonSerializable()
class Grade {
  final String gName;
  final String cName;

  Grade(this.gName, this.cName);

  factory Grade.fromJson(Map<String, dynamic> json) => _$GradeFromJson(json);
  Map<String, dynamic> toJson() => _$GradeToJson(this);
}
```

写好以后执行生成命令：

```bash
dart run build_runner build
# 或者
flutter packages pub run build_runner build
# watch 会在项目根目录持续监听，如果创建新的Model会自动生成。
flutter packages pub run build_runner build watch
```

生成的Model字段被强制`as` 为字符串类型`String`。

```dart
part of 'user.dart';

// **************************************************************************
// JsonSerializableGenerator
// **************************************************************************

User _$UserFromJson(Map<String, dynamic> json) {
  return User(
    json['name'] as String,
    json['age'] as String,
    Grade.fromJson(json['grade'] as Map<String, dynamic>),
  );
}

Map<String, dynamic> _$UserToJson(User instance) => <String, dynamic>{
      'name': instance.name,
      'age': instance.age,
      'grade': instance.grade,
    };

Grade _$GradeFromJson(Map<String, dynamic> json) {
  return Grade(
    json['gName'] as String,
    json['cName'] as String,
  );
}

Map<String, dynamic> _$GradeToJson(Grade instance) => <String, dynamic>{
      'gName': instance.gName,
      'cName': instance.cName,
    };
```


```
.
├── user.dart
└── user.g.dart # 生成的代码
```

### 枚举

```dart
enum LocationType {
  @JsonValue('City')
  city,
  @JsonValue('Region')
  region,
  @JsonValue('Continent')
  continent
}

@JsonSerializable()
class Location {
  const Location({required this.locationType});
  final LocationType locationType;
}
```

其中枚举`LocationType`中的每个字段中都写了对应的`JsonValue`， 具体含义就是在Model `Location`中给字段`locationType`赋值时，把对应的String类型（例：`City`）转成对应枚举的值。

# json_serializable

## @JsonValue 基础使用

```dart
class JsonKey {
  final Object? defaultValue; // 设置字段默认值，默认值 null
  final bool? disallowNullValue;
  final Function? fromJson;
  final bool? ignore;
  final bool? includeIfNull;
  final String? name; // 字段名映射
  final bool? required;
  final Function? toJson;
  final Object? unknownEnumValue;// 默认未知枚举值
}
```

```dart
@JsonKey(name: 'weather_state_abbr', unknownEnumValue: WeatherState.unknown)
String weatherStateAbbr;
```

把服务器下发的字段`weather_state_abbr`序列化成模型字段`weatherStateAbbr`。`unknownEnumValue` 参数是默认指派一个未知的枚举值`WeatherState.unknown`。
