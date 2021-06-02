
> [自适应应用](https://flutter.cn/docs/development/ui/layout/building-adaptive-apps) 是 `Flutter2.2` 版本以后新增的功能。

# 创建自适应布局

## VisualDensity 布局

[VisualDensity](https://api.flutter-io.cn/flutter/material/VisualDensity-class.html)

## 上下文布局

### 使用界面像素尺寸进行布局

### 使用 LayoutBuilder 进行定制布局

[LayoutBuilder](https://api.flutter-io.cn/flutter/widgets/LayoutBuilder-class.html) 构建一个依赖于父Widget大小约束的Widget。

<iframe width="560" height="315" src="https://www.youtube.com/embed/IYDVcriKjsw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

```dart
class LayoutBuilderExample extends StatelessWidget {
  const LayoutBuilderExample({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return LayoutBuilder(
      builder: (BuildContext context, BoxConstraints constraints) {
        bool useVerticalLayout = constraints.maxWidth < 400.0;
        return Flex(
          direction: useVerticalLayout ? Axis.vertical : Axis.horizontal,
          children: [],
        );
      },
    );
  }
}
```

### 分析设备

[Platform](https://api.flutter-io.cn/flutter/package-platform_platform/Platform-class.html) 可以让开发者弄清楚当前是那个平台，通过区分不同的平台去进行布局。

```dart
class DevicesExample extends StatelessWidget {
  const DevicesExample({Key? key}) : super(key: key);

  bool get isMobileDevice => (Platform.isIOS || Platform.isAndroid);
  bool get isMobileDeviceOrWeb => isMobileDevice || kIsWeb;

  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```

在 Web 端使用`Platform`时会抛出异常，可以使用[universal_platform](https://pub.flutter-io.cn/packages/universal_platform)。

```dart
void initState() {
  try {
    bool devices = (Platform.isIOS || Platform.isAndroid);
  } catch (e) {
    print('===>$e');
  }
  super.initState();
}
// 报错：===>Unsupported operation: Platform._operatingSystem
```




