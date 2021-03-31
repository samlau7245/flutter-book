
# Package

## 新建Package

```sh
dart create --template package-simple /Users/dart/Desktop/core_extension
```

创建出的目录结构：

```
├── CHANGELOG.md
├── README.md
├── analysis_options.yaml
├── example
│ └── core_extension_example.dart
├── lib
│ ├── core_extension.dart
│ └── src
│     └── core_extension_base.dart
├── pubspec.lock
├── pubspec.yaml
└── test
    └── core_extension_test.dart
```

## 创建文档

```sh
# 搭建 dartdoc 环境
dart pub global activate dartdoc
# cd 到 package根目录下
cd /Users/dart/Desktop/core_extension
# 生成 Library 文档
dart pub global run dartdoc
```