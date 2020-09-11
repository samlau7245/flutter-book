
[ClipRRect-class](https://api.flutter.dev/flutter/widgets/ClipRRect-class.html)

# 构造函数

```dart
ClipRRect({
	Key key, 
	BorderRadius borderRadius: BorderRadius.zero, // 边框半径裁剪
	CustomClipper<RRect> clipper, 
	Clip clipBehavior: Clip.antiAlias, 
	Widget child
})
```

# 示例

```dart
ClipRRect(
  borderRadius: BorderRadius.circular(6),
  child: Image.network(
    "https://img1.gamersky.com/image2019/07/20190725_ll_red_136_2/gamersky_07small_14_201972510258D0.jpg",
    width: 130,
    height: 180,
    fit: BoxFit.cover,
  ),
)
```

 下面图片就是添加圆角和没有添加圆角的区别：

<img src="/assets/images/widgets/54.png"/>