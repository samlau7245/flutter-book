
# Flutter 2.2(2021-05-19)

## 空安全支持

从`Flutter 2.2`开始，新创建项目将 **默认启用健全的空安全**。

* [null-safety](https://dart.cn/null-safety)

## 平台优化

### Web

从`Flutter 2.2`开始，提供了`Service Worker`以进行后台缓存。

可视化调节语法树：

```bash
flutter run -d chrome --profile --dart-define = FLUTTER_WEB_DEBUG_SHOW_SEMANTICS = true
```

### Android

新增[延迟加载组件](https://flutter.cn/docs/perf/deferred-components)

### iOS

[着色器的预编译](https://flutter.cn/docs/perf/rendering/shader#how-to-use-sksl-warmup)集成至开发工具中，可以消除或减少首次运行的卡顿。

## 新业务

* [新广告SDK插件](https://pub.flutter-io.cn/packages/google_mobile_ads)
* [支持支付插件(Google Pay、Apple Pay)](https://pub.flutter-io.cn/packages/google_mobile_ads)

## Dart 2.13

* [Medium: Announcing Dart 2.13](https://medium.com/dartlang/announcing-dart-2-13-c6d547b57067)

### 重命名类名

```dart
@Deprecated('Use NewValueChanged instead!')
typedef ValueChanged<T> = void Function(T value);
```

## 图标

* [Google Icons](fonts.google.com/icons)