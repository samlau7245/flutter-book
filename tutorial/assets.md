
> Flutter 官方教程： https://flutter.cn/docs/development/ui/assets-and-images

# 配置资源路径

## 指定单个文件

```yaml
name: xxx
dependencies:
flutter:
  assets:
    - assets/contects.json # JSON资源文件
```

对应的文件夹结构：

```
.
├── assets
│   └── contects.json
├── lib
│   └── main.dart
└── pubspec.yaml
```

## 指定文件夹

# 加载资源

## 加载文本资源

```dart
import 'dart:async' show Future;
import 'package:flutter/services.dart' show rootBundle;

Future<String> loadAsset() async {
  return await rootBundle.loadString('assets/contects.json');
}
```
