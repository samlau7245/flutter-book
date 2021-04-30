# 平台

## Platform

在`Platform`类中可以获取当前平台判断:

```dart
static final bool isLinux = (_operatingSystem == "linux");
static final bool isMacOS = (_operatingSystem == "macos");
static final bool isWindows = (_operatingSystem == "windows");
static final bool isAndroid = (_operatingSystem == "android");
static final bool isIOS = (_operatingSystem == "ios");
static final bool isFuchsia = (_operatingSystem == "fuchsia");
```

```dart
import 'dart:io' as io;
void main() {
  if (io.Platform.isMacOS) {};
}
```

[flutter_platform_widgets]()

# 显示

## MediaQuery

`MediaQuery`继承与`InheritedWidget`，所以你可以从任何一个`widget tree`中获取到`MediaQuery`。

```dart
@override
idget build(BuildContext context) {
 final mediaQuery = MediaQuery.of(context);
}
```

可以根据界面的`MediaQuery.size`属性，来适配界面的变化。

```dart
@override
Widget build(BuildContext context) {
    final mediaQuery = MediaQuery.of(context);

    if (mediaQuery.size.width > 1024) {
      return LargeLayout();
    }

    if (mediaQuery.size.width > 332) {
      return MediumLayout();
    }

    return SmallLayout();
}
```

### 像素兼容

```dart
@override
Widget build(BuildContext context) {
    final mediaQuery = MediaQuery.of(context);

    if (mediaQuery.devicePixelRatio >= 2) {
      return HighDefinitionVideo();
    }

    return LowDefinitionVideo();
}
```

### 界面安全区域



## Screen dimensions 屏幕的维度

<img src="/assets/images/layout/01.png"/>

# 参考

* [视频: 宣布推出新的 Flutter Folio 应用程序](https://youtu.be/x4xZkdlADWo)
* [Folio 的源代码](https://github.com/gskinnerTeam/flutter-folio)
* [博文和视频](https://aloisdeniel.com/#/posts/adaptative-ui)

