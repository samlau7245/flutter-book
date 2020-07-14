
> **[danger] 注意**
>
> 如果使用了 Flutter SDK 就不能直接使用 `pub` 命令，需要使用 `flutter pub`。[Flutter Packages](https://flutter.cn/docs/development/packages-and-plugins)

# 创建Packages 

## 纯Dart(Dart packages)

使用纯Dart语言写的packages，使用范围仅限于Flutter。

```sh
$ flutter create --template=package hello
```

创建成功后项目的数结构:

```
hello
├── CHANGELOG.md # 用于记录 package 的版本变更。
├── LICENSE # 空的一个许可证文件
├── README.md # 用于描述 package。
├── hello.iml # 由 IntelliJ 生成的配置文件
├── lib
│   └── hello.dart # package 的 Dart 实现代码。
├── pubspec.lock # 
├── pubspec.yaml # pub 工具需要使用的，包含 package 依赖的 yaml 格式的文件
└── test
    └── hello_test.dart # 单元测试 文件
```

## 原生插件(Plugin packages)

要开发一个调用特定平台 API 的 package,就需要开发一个原生插件packgae。除了要实现 Dart package 要实现的内容，还需要按需使用 Java 或 Kotlin、ObjC 或 Swift 分别在 Android 和/或 iOS 平台实现，你可以使用 [platform channels](https://flutter.cn/docs/development/platform-integration/platform-channels)中的 API 来实现特定平台的调用。

### 创建 package

```sh
$ flutter create --org com.example --template=plugin -a kotlin hello
# 或者
$ flutter create --org com.example --template=plugin -a java hello
# 或者
$ flutter create --org com.example --template=plugin -i objc hello
# 或者
$ flutter create --org com.example --template=plugin -i swift hello
```

Package的树结构：

``` sh
hello
├── CHANGELOG.md
├── LICENSE
├── README.md
├── example # 一个依赖于该插件并说明了如何使用它的 Flutter 应用
├── hello.iml
├── ios
│   ├── Assets
│   ├── Classes
│   │   ├── HelloPlugin.h # iOS 平台原生插件 API 实现
│   │   └── HelloPlugin.m # iOS 平台原生插件 API 实现
│   └── hello.podspec
├── lib
│   └── hello.dart # Dart 插件 API 实现
├── pubspec.lock
├── pubspec.yaml
└── test
    └── hello_test.dart
```

### 指定插件支持平台

在`pubspec.yaml`中指定一个插件支持的平台。

```yaml
flutter:
  # 指定插件的支持的平台：[ios (default), android (default), windows (default), linux (default), macos (default), web (default)]
  plugin:
    platforms:
      android:
        package: com.example.hello
        pluginClass: HelloPlugin
      ios:
        pluginClass: HelloPlugin
      macos:
        pluginClass: HelloPlugin
      web:
        pluginClass: HelloPlugin
        fileName: hello_web.dart
```

再次执行: `flutter create --org com.example --template=plugin ...` 创建插件的命令。可以创建其他平台的插件。

### package 添加iOS平台代码

使用 Xcode 编辑 iOS 平台代码之前，首先确保代码至少被构建过一次：

```sh
$ cd hello/example
$ flutter build ios --no-codesign
```

插件的 iOS 平台代码位于项目导航中的这个位置:`Pods/Development Pods/hello/../../example/ios/.symlinks/plugins/hello/ios/Classes`

<img src="/assets/images/package/01.png"/>

# 发布到 pub.dev

在发布 package 之前，确保检查了这几个文件：`pubspec.yaml`、`README.md` 和 `CHANGELOG.md`，确保它们完整。

```sh
# 检验是否所有内容都通过了分析
$ flutter pub publish --dry-run

# 最后一步是发布，请注意：发布是永久性 的
$ flutter pub publish
# 或者
$ flutter pub publish --server=https://pub.dartlang.org
```

# package 依赖

如果当前正在开发的 `hello` Package，需要依赖另外一个 `url_launcher` Package，需要将 `url_launcher` 添加到文件 `pubspec.yaml` 的 `dependencies` 字段中。

## 依赖纯Dart插件

```yaml
dependencies:
  url_launcher: ^5.0.0
```

## 依赖原生插件

### iOS

在 `hello/ios/hello.podspec` 文件中为 `url_launcher` 插件设定依赖关系。

```ruby
Pod::Spec.new do |s|
  s.dependency 'url_launcher'
```

<img src="/assets/images/package/02.png"/>

# 依赖源

## 路径

项目路径树:

```sh
.
├── demo # 项目，在 demo 中使用 package_a
│   ├── README.md
│   ├── android
│   ├── ios
│   ├── lib
│   │   └── main.dart
│   ├── macos
│   ├── pubspec.lock
│   ├── pubspec.yaml
│   ├── test
│   ├── web
│   └── windows
└── package_a # package
    ├── lib
    │   └── package_a.dart
    ├── package_a.iml
    ├── pubspec.lock
    ├── pubspec.yaml
    └── test
        └── package_a_test.dart
```

 配置 demo 中 `podspec.yaml` 的依赖：

```yaml
dependencies:
  flutter:
    sdk: flutter
  package_a:
    path: /Users/sam/Documents/Dart/package_dart/package_a
```

demo 中使用 package:

```dart
import 'package:package_a/package_a.dart';

class _MyHomePageState extends State<MyHomePage> {
  void _incrementCounter() {
    setState(() {
      Calculator cal = Calculator();
      cal.addOne(1);
    });
  }
}
```

`package_a.dart`中的代码：

```dart
library package_a;

class Calculator {
  int addOne(int value) => value + 1;
}
```

## Git

[详细的Git依赖可以参考官方](https://dart.cn/tools/pub/dependencies)

配置 demo 中 `podspec.yaml` 的依赖：

```yaml
dependencies:
  flutter:
    sdk: flutter
  package_b:
    git: https://gitee.com/package_mo/package_b.git
    # ref: some-branch
```























