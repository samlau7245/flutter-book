
* [TextStyle class](https://api.flutter.dev/flutter/material/TextStyle-class.html)

# 构造函数

```dart
TextStyle({
	Color color, 颜色 
	TextDecoration decoration, 添加上划线，下划线，删除线 
	Color decorationColor, 划线的颜色
	TextDecorationStyle decorationStyle, 这个style可能控制画实线，虚线，两条线，点, 波浪线等
	double decorationThickness,
	FontWeight fontWeight, 字重，加粗也用这个字段  FontWeight.w700 
	FontStyle fontStyle,FontStyle.normal  FontStyle.italic斜体
	TextBaseline textBaseline, 基线，两个值，字面意思是一个用来排字母的，一人用来排表意字的（类似中文）
	String fontFamily, 字体
	List<String> fontFamilyFallback,
	double fontSize,字号
	double letterSpacing, 字符间距  就是单个字母或者汉字之间的间隔，可以是负数
	double wordSpacing, 字间距 句字之间的间距
	double height, 当用来Text控件上时，行高（会乘以fontSize,所以不以设置过大） lineHeight = fontSize * height
	Locale locale,
	Paint background,
	Paint foreground,
	List<Shadow> shadows,
	List<FontFeature> fontFeatures
})
```

## TextDecoration 划线

<img src="/assets/images/widgets/43.png"/>

## TextDecorationStyle 线样式

```dart
enum TextDecorationStyle {
  solid, ///画一条直线
  double, /// 画两条线
  dotted, /// 画圆点虚线
  dashed, /// 画破折号虚线
  wavy /// 画波浪线
}
```

<img src="/assets/images/widgets/44.png"/>

# 示例

<img src="/assets/images/widgets/01.png"/>

[TypePageExample.dart](https://gitee.com/SamLearning/FlutterExample/blob/master/widgets/lib/class/TypePageExample.dart)

```dart
import 'dart:ui';
import 'package:flutter/material.dart';

class TypePageExample extends StatelessWidget {

  final titleStyle = TextStyle(
    fontSize: 18,
    fontFeatures: [FontFeature.enable('smcp')],
    color: Colors.blueGrey[600],
  );

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("TextStyleExample"),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Spacer(flex: 5),
            Text('regular numbers have their place:', style: titleStyle),
            Text('The 1972 cup final was a 1-1 draw.',
                style: TextStyle(
                  fontFamily: 'Cardo',
                  fontSize: 24,
                )),
            Spacer(),
            Text('but old-style figures blend well with lower case:',
                style: titleStyle),
            Text('The 1972 cup final was a 1-1 draw.',
                style: TextStyle(
                    fontFamily: 'Cardo',
                    fontSize: 24,
                    fontFeatures: [FontFeature.oldstyleFigures()])),
            Spacer(),
            Divider(),
            Spacer(),
            Text('fractions look better with a custom ligature:',
                style: titleStyle),
            Text('Add 1/2 tsp of flour and stir.',
                style: TextStyle(
                    fontFamily: 'Milonga',
                    fontSize: 24,
                    fontFeatures: [FontFeature.enable('frac')])),
            Spacer(),
            Divider(),
            Spacer(),
            Text('multiple stylistic sets in one font:', style: titleStyle),
            Text('Raleway Dots',
                style: TextStyle(fontFamily: 'Raleway Dots', fontSize: 48)),
            Text('Raleway Dots',
                style: TextStyle(
                  fontFeatures: [FontFeature.stylisticSet(1)],
                  fontFamily: 'Raleway Dots',
                  fontSize: 48,
                )),
            Spacer(flex: 5),
          ],
        ),
      ),
    );
  }
}
```
