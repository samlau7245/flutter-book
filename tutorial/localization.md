
> 可以实现国际化的Package：[intl](https://pub.flutter-io.cn/packages/intl)、[flutter_localizations](https://pub.flutter-io.cn/packages/flutter_localizations)。


# 步骤

## 添加依赖

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
```

## 设置语言环境和支持的库

```dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      home: Home(),
      /// `localizationsDelegates`数组: 用于生成本地化值集合的工厂
      localizationsDelegates: [
        GlobalMaterialLocalizations.delegate, // 为 Material 组件库提供本地化的字符串和一些其他的值。
        GlobalWidgetsLocalizations.delegate, // 为 widgets 库定义了默认的文本排列方向，由左到右或者由右到左。
        GlobalCupertinoLocalizations.delegate, // 为 Cupertial 组件库提供本地化的字符串和一些其他的值。
      ],
      supportedLocales: [
        const Locale('en'), // Locale 支持的语言环境
        const Locale('es'),
      ],
    );
  }
}
```

* `supportedLocales`数组: 表示可以支持的语言环境，可以使用`Locale()`、或者`Locale.fromSubtags()`。
* `localizationsDelegates`数组: 用于生成本地化值集合的工厂。

## 添加本地化信息

* 新增`intl`依赖： `flutter pub add intl`。
* 启动`generate`标志。

```yaml
flutter:
  generate: true
```

## 添加本地化配置文件

在项目根目录创建`l10n.yaml`：

```
├── l10n.yaml
├── lib
└── pubspec.yaml
```

编辑`l10n.yaml`配置文件：

```yaml
# 在 `/lib/l10n` 路径的文件夹中，`app_en.arb`文件提供模版，生成的本地化文件保存在`app_localizations.dart`文件中。
arb-dir: lib/l10n
template-arb-file: app_en.arb
output-localization-file: app_localizations.dart
```

创建两个语言模版文件：`app_en.arb`、`app_es.arb`

```yaml
├── l10n.yaml
├── lib
│     ├── l10n
│     │     ├── app_es.arb
│     │     └── app_en.arb
│     └── main.dart
└── pubspec.yaml
```

在`app_en.arb`模版文件中创建模版内容：

```dart
{
    "helloWorld": "Hello World!",
    "@helloWorld": {
      "description": "The conventional newborn programmer greeting"
    }
}
```

在`app_es.arb`模版文件中创建模版内容：

```dart
{
    "helloWorld": "Hola Mundo!"
}
```

```bash
flutter pub global activate intl_translation
flutter pub run intl_translation:extract_to_arb --output-dir=lib/l10n lib/main.dart
```


* [Guide for building internationalized Flutter apps](https://docs.google.com/document/d/10e0saTfAv32OZLRmONy866vnaw0I2jwL8zukykpgWBc/edit)