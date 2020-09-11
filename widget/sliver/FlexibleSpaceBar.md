
[FlexibleSpaceBar Class](https://api.flutter.dev/flutter/material/FlexibleSpaceBar-class.html)

# 构造函数

```dart
const FlexibleSpaceBar({
	Key key,
	Widget title,
	Widget background,
	bool centerTitle,
	EdgeInsetsGeometry titlePadding,
	CollapseMode collapseMode: CollapseMode.parallax,
	List<StretchMode> stretchModes: const [StretchMode.zoomBackground]
})
```

# 示例

```dart
import 'package:flutter/material.dart';

class FlexibleSpaceBarExample extends StatefulWidget {
  @override
  _FlexibleSpaceBarExampleState createState() =>
      _FlexibleSpaceBarExampleState();
}

class _FlexibleSpaceBarExampleState extends State<FlexibleSpaceBarExample> {
  @override
  Widget build(BuildContext context) {
    return CustomScrollView(
      slivers: [
        SliverAppBar(
          stretch: true,
          onStretchTrigger: () {
            // Function callback for stretch
            return;
          },
          expandedHeight: 300.0,
          flexibleSpace: FlexibleSpaceBar(
            stretchModes: <StretchMode>[
              StretchMode.zoomBackground,
              StretchMode.blurBackground,
              StretchMode.fadeTitle,
            ],
            centerTitle: true,
            title: const Text('Flight Report'),
            background: Stack(
              fit: StackFit.expand,
              children: [
                Image.network(
                  'https://flutter.github.io/assets-for-api-docs/assets/widgets/owl-2.jpg',
                  fit: BoxFit.cover,
                ),
                const DecoratedBox(
                  decoration: BoxDecoration(
                    gradient: LinearGradient(
                      begin: Alignment(0.0, 0.5),
                      end: Alignment(0.0, 0.0),
                      colors: <Color>[
                        Color(0x60000000),
                        Color(0x00000000),
                      ],
                    ),
                  ),
                ),
              ],
            ),
          ),
        ),
      ],
    );
  }
}
```


<img src="/assets/images/widgets/17.png"/>