
# [ThemeData](https://api.flutter.dev/flutter/material/ThemeData-class.html)

```dart
Theme(
  data: ThemeData(primaryColor: Colors.amber),
  child: Builder(
    builder: (BuildContext context) {
      return Container(
        width: 100,
        height: 100,
        color: Theme.of(context).primaryColor, // 获取到上下文中的主题数据
      );
    },
  ),
)
```

<img src="/assets/images/flutter/80.png" width = "50%" height = "50%"/>

```dart
MaterialApp(
  // 这里设置了全局主题数据
  theme: ThemeData(
    primaryColor: Colors.blue, // 全局主题色
    accentColor: Colors.green, // 全局强调色
    textTheme: TextTheme(bodyText2: TextStyle(color: Colors.purple)), // 全局字体色
  ),
  home: Scaffold(
    appBar: AppBar(
      title: const Text('ThemeData Demo'),
    ),
    floatingActionButton: FloatingActionButton(
      child: const Icon(Icons.add),
      onPressed: () {},
    ),
    body: Center(
      child: Text(
        'Button pressed 0 times',
      ),
    ),
  ),
)
```

|属性名|类型|描述|
| --- | --- |--- |
| `brightness` | [Brightness](https://api.flutter.dev/flutter/material/Brightness-class.html) | |
| `visualDensity` | [VisualDensity](https://api.flutter.dev/flutter/material/VisualDensity-class.html) | |
| `primarySwatch` | [MaterialColor](https://api.flutter.dev/flutter/material/MaterialColor-class.html) | |
| `primaryColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) |主题色 |
| `primaryColorBrightness` | [Brightness](https://api.flutter.dev/flutter/material/Brightness-class.html) | |
| `primaryColorLight` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `primaryColorDark` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `accentColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) |强调色 |
| `accentColorBrightness` | [Brightness](https://api.flutter.dev/flutter/material/Brightness-class.html) | |
| `canvasColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `scaffoldBackgroundColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `bottomAppBarColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `cardColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `dividerColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `focusColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `hoverColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `highlightColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `splashColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `splashFactory` | [InteractiveInkFeatureFactory](https://api.flutter.dev/flutter/material/InteractiveInkFeatureFactory-class.html) | |
| `selectedRowColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `unselectedWidgetColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `disabledColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `buttonColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `buttonTheme` | [ButtonThemeData](https://api.flutter.dev/flutter/material/ButtonThemeData-class.html) | |
| `toggleButtonsTheme` | [ToggleButtonsThemeData](https://api.flutter.dev/flutter/material/ToggleButtonsThemeData-class.html) | |
| `secondaryHeaderColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `textSelectionColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `cursorColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `textSelectionHandleColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `backgroundColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `dialogBackgroundColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `indicatorColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `hintColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `errorColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `toggleableActiveColor` | [Color](https://api.flutter.dev/flutter/material/Color-class.html) | |
| `fontFamily` | [String](https://api.flutter.dev/flutter/material/String-class.html) | |
| `textTheme` | [TextTheme](https://api.flutter.dev/flutter/material/TextTheme-class.html) | |
| `primaryTextTheme` | [TextTheme](https://api.flutter.dev/flutter/material/TextTheme-class.html) | |
| `accentTextTheme` | [TextTheme](https://api.flutter.dev/flutter/material/TextTheme-class.html) | |
| `inputDecorationTheme` | [InputDecorationTheme](https://api.flutter.dev/flutter/material/InputDecorationTheme-class.html) | |
| `iconTheme` | [IconThemeData](https://api.flutter.dev/flutter/material/IconThemeData-class.html) | |
| `primaryIconTheme` | [IconThemeData](https://api.flutter.dev/flutter/material/IconThemeData-class.html) | |
| `accentIconTheme` | [IconThemeData](https://api.flutter.dev/flutter/material/IconThemeData-class.html) | |
| `sliderTheme` | [SliderThemeData](https://api.flutter.dev/flutter/material/SliderThemeData-class.html) | |
| `tabBarTheme` | [TabBarTheme](https://api.flutter.dev/flutter/material/TabBarTheme-class.html) | |
| `tooltipTheme` | [TooltipThemeData](https://api.flutter.dev/flutter/material/TooltipThemeData-class.html) | |
| `cardTheme` | [CardTheme](https://api.flutter.dev/flutter/material/CardTheme-class.html) | |
| `chipTheme` | [ChipThemeData](https://api.flutter.dev/flutter/material/ChipThemeData-class.html) | |
| `platform` | [TargetPlatform](https://api.flutter.dev/flutter/material/TargetPlatform-class.html) | |
| `materialTapTargetSize` | [MaterialTapTargetSize](https://api.flutter.dev/flutter/material/MaterialTapTargetSize-class.html) | |
| `applyElevationOverlayColor` | [bool](https://api.flutter.dev/flutter/material/bool-class.html) | |
| `pageTransitionsTheme` | [PageTransitionsTheme](https://api.flutter.dev/flutter/material/PageTransitionsTheme-class.html) | |
| `appBarTheme` | [AppBarTheme](https://api.flutter.dev/flutter/material/AppBarTheme-class.html) | |
| `bottomAppBarTheme` | [BottomAppBarTheme](https://api.flutter.dev/flutter/material/BottomAppBarTheme-class.html) | |
| `colorScheme` | [ColorScheme](https://api.flutter.dev/flutter/material/ColorScheme-class.html) | |
| `dialogTheme` | [DialogTheme](https://api.flutter.dev/flutter/material/DialogTheme-class.html) | |
| `floatingActionButtonTheme` | [FloatingActionButtonThemeData](https://api.flutter.dev/flutter/material/FloatingActionButtonThemeData-class.html) | |
| `navigationRailTheme` | [NavigationRailThemeData](https://api.flutter.dev/flutter/material/NavigationRailThemeData-class.html) | |
| `typography` | [Typography](https://api.flutter.dev/flutter/material/Typography-class.html) | |
| `cupertinoOverrideTheme` | [CupertinoThemeData](https://api.flutter.dev/flutter/material/CupertinoThemeData-class.html) | |
| `snackBarTheme` | [SnackBarThemeData](https://api.flutter.dev/flutter/material/SnackBarThemeData-class.html) | |
| `bottomSheetTheme` | [BottomSheetThemeData](https://api.flutter.dev/flutter/material/BottomSheetThemeData-class.html) | |
| `popupMenuTheme` | [PopupMenuThemeData](https://api.flutter.dev/flutter/material/PopupMenuThemeData-class.html) | |
| `bannerTheme` | [MaterialBannerThemeData](https://api.flutter.dev/flutter/material/MaterialBannerThemeData-class.html) | |
| `dividerTheme` | [DividerThemeData](https://api.flutter.dev/flutter/material/DividerThemeData-class.html) | |
| `buttonBarTheme` | [ButtonBarThemeData](https://api.flutter.dev/flutter/material/ButtonBarThemeData-class.html) | |
