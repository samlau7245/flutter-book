
* [TextStyle class](https://api.flutter.dev/flutter/material/TextStyle-class.html)

# 构造函数

```dart
TextStyle({
	Color color,
	TextDecoration decoration,
	Color decorationColor,
	TextDecorationStyle decorationStyle,
	double decorationThickness,
	FontWeight fontWeight,
	FontStyle fontStyle,
	TextBaseline textBaseline,
	String fontFamily,
	List<String> fontFamilyFallback,
	double fontSize,
	double letterSpacing,
	double wordSpacing,
	double height,
	Locale locale,
	Paint background,
	Paint foreground,
	List<Shadow> shadows,
	List<FontFeature> fontFeatures
})
```

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
