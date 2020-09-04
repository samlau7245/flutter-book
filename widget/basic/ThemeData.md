
[ThemeData Class](https://api.flutter.dev/flutter/material/ThemeData-class.html)

# 构造函数

```dart
ThemeData({
  Color secondaryHeaderColor, 有选定行时PaginatedDataTable标题的颜色。
  Color textSelectionColor, 文本字段中选中文本的颜色，例如TextField。
  Color cursorColor, 输入框光标颜色。
  Color textSelectionHandleColor, 用于调整当前文本的哪个部分的句柄颜色。
  Color backgroundColor,// 与primaryColor对比的颜色(例如 用作进度条的剩余部分)。
  Color dialogBackgroundColor, Dialog元素的背景色。
  Color indicatorColor, TabBar中选项选中的指示器颜色。
  Color hintColor, 用于提示文本或占位符文本的颜色，例如在TextField中。
  Color errorColor, 用于输入验证错误的颜色，例如在TextField中。
  Color toggleableActiveColor, 用于突出显示切换Widget（如Switch，Radio和Checkbox）的活动状态的颜色。
  Color primaryColor, App主要部分的背景色（ToolBar,TabBar等）。
  Color primaryColorLight, primaryColor的高亮版本。
  Color primaryColorDark, primaryColor的较暗版本。
  Color accentColor, // 前景色（文本、按钮等）
  Color canvasColor,// MaterialType.canvas Material的默认颜色。
  Color scaffoldBackgroundColor, 作为Scaffold基础的Material默认颜色，典型Material应用或应用内页面的背景颜色。
  Color bottomAppBarColor, // BottomAppBar的默认颜色
  Color cardColor, Material被用作Card时的颜色。
  Color dividerColor, Dividers和PopupMenuDividers的颜色，也用于ListTiles中间，和DataTables的每行中间.
  Color focusColor, 焦点获取时的颜色，例如，一些按钮焦点、输入框焦点。
  Color hoverColor, 点击之后徘徊中的颜色，例如，按钮长按，按住之后的颜色。
  Color highlightColor, 用于类似墨水喷溅动画或指示菜单被选中的高亮颜色。
  Color splashColor, 墨水喷溅的颜色。
  Color selectedRowColor, 选中行时的高亮颜色。
  Color unselectedWidgetColor, 用于Widget处于非活动（但已启用）状态的颜色。 例如，未选中的复选框。 通常与accentColor形成对比。
  Color disabledColor, 用于Widget无效的颜色，无论任何状态。例如禁用复选框。
  Color buttonColor, Material中RaisedButtons使用的默认填充色。

  TextTheme textTheme, // 字体主题，包括标题、body等文字样式
  TextTheme primaryTextTheme,
  TextTheme accentTextTheme,
  InputDecorationTheme inputDecorationTheme,
  TabBarTheme tabBarTheme,
  CardTheme cardTheme,
  PageTransitionsTheme pageTransitionsTheme,
  AppBarTheme appBarTheme,
  BottomAppBarTheme bottomAppBarTheme,
  DialogTheme dialogTheme,

  ButtonThemeData buttonTheme, //按钮主题
  ToggleButtonsThemeData toggleButtonsTheme,
  IconThemeData iconTheme, // Icon的默认样式
  IconThemeData primaryIconTheme,
  IconThemeData accentIconTheme,
  SliderThemeData sliderTheme,
  TooltipThemeData tooltipTheme,
  ChipThemeData chipTheme,
  FloatingActionButtonThemeData floatingActionButtonTheme,
  NavigationRailThemeData navigationRailTheme,
  CupertinoThemeData cupertinoOverrideTheme,
  SnackBarThemeData snackBarTheme,
  BottomSheetThemeData bottomSheetTheme,
  PopupMenuThemeData popupMenuTheme,
  MaterialBannerThemeData bannerTheme,
  DividerThemeData dividerTheme,
  ButtonBarThemeData buttonBarTheme,
  BottomNavigationBarThemeData bottomNavigationBarTheme,
  TimePickerThemeData timePickerTheme,

  Brightness brightness, Brightness类型，应用程序整体主题的亮度。 由按钮等Widget使用，以确定在不使用主色或强调色时要选择的颜色。
  VisualDensity visualDensity,
  MaterialColor primarySwatch,
  Brightness primaryColorBrightness,// 主题主色的深浅色
  Brightness accentColorBrightness, Brightness类型，accentColor的亮度。 用于确定放置在突出颜色顶部的文本和图标的颜色（例如FloatingButton上的图标）。
  InteractiveInkFeatureFactory splashFactory, InteractiveInkFeatureFactory类型，定义InkWall和InkResponse生成的墨水喷溅的外观。
  String fontFamily,//文字字体
  TargetPlatform platform,  //指定平台，应用特定平台控件风格
  MaterialTapTargetSize materialTapTargetSize, Chip等组件的尺寸主题设置，如：设置为MaterialTapTargetSize.shrinkWrap时，clip距顶部距离为0；设置为MaterialTapTargetSize.padded时距顶部有一个距离
  bool applyElevationOverlayColor, 是否应用elevation覆盖颜色。
  ColorScheme colorScheme, scheme组颜色，一组13种颜色，可用于配置大多数组件的颜色属性。
  Typography typography, 用于配置TextTheme、primaryTextTheme和accentTextTheme的颜色和几何文本主题值。
  bool fixTextFieldOutlineLabel
})
```

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