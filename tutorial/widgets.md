# Stateless Widgets

<iframe width="560" height="315" src="https://www.youtube.com/embed/wE7khGHVkYY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Stateful Widgets

<iframe width="560" height="315" src="https://www.youtube.com/embed/AqCMFXEmf3w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# InheritedWidget

`InheritedWidget`是所有 widgets 的基类，这样可以在 widgets 底层树中有效的传播信息。

<img src="/assets/images/widgets/01.png"/>

<img src="/assets/images/widgets/02.png"/>


示例：

```dart
class InheritedNose extends InheritedWidget {
  final Widget child;
  final Image asset;
  InheritedNose({this.asset, this.child}) : super(child: child);

  @override
  bool updateShouldNotify(covariant InheritedWidget oldWidget) => true;
}
```

我们创建一个自定义[InheritedWidget](https://api.flutter.dev/flutter/widgets/InheritedWidget-class.html)的 widget `InheritedNose`，它有个一个 Data 就是一个图片`asset`；现在我们要在其他的 Widget 中使用 `InheritedNose` 的 Data：

```dart
class FilipWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final nose = context.dependOnInheritedWidgetOfExactType<InheritedNose>();
    nose.asset;
    return Container();
  }
}
```

这样我们通过 [dependOnInheritedWidgetOfExactType](https://api.flutter.dev/flutter/widgets/BuildContext/dependOnInheritedWidgetOfExactType.html) 就可以获取到`InheritedNose`的数据。

我们可以对 `InheritedNose` 进一步的优化：

```dart
class InheritedNose extends InheritedWidget {
  //...
  static InheritedNose of(BuildContext context) =>
      context.dependOnInheritedWidgetOfExactType<InheritedNose>();
}
```

给`InheritedNose`中添加一个`of`的静态方法，这样外部就可以直接执行`of`获取`InheritedNose`中的 Data 了。

```dart
class FilipWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final ret = InheritedNose.of(context).asset;
    return Container();
  }
}
```

具体的示例：


```dart
class InheritedDemoColor extends InheritedWidget {
  final Color color;
  final Widget child;

  InheritedDemoColor({this.color, this.child}) : super(child: child);

  @override
  bool updateShouldNotify(covariant InheritedDemoColor old) =>
      old.color != color;

  static InheritedDemoColor of(BuildContext context) {
    final ret =
        context.dependOnInheritedWidgetOfExactType<InheritedDemoColor>();
    assert(ret != null, 'No InheritedDemoColor found in context');
    return ret;
  }
}

class DemoWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: InheritedDemoColor(
        color: Colors.red,
        child: Text(
          'demo',
          style: TextStyle(color: InheritedDemoColor.of(context).color),
        ),
      ),
    );
  }
}
```

具体可以参考官方视频：

<iframe width="560" height="315" src="https://www.youtube.com/embed/Zbm3hjPjQMk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Keys

<iframe width="560" height="315" src="https://www.youtube.com/embed/kn0EOS-ZiIc" title="YouTube video player" frameborder="0" a llow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

* [flutter-cn:Keys](https://flutter.cn/docs/development/ui/widgets-intro#keys)

* `Local Keys` 在构建相同类型 widget 的多个实例时很有用，类似于 UITableView的`dequeueReusableCellWithIdentifier:(NSString *)identifier`中的 `identifier` 重用标识符号。
* `Global Keys` 可以用来标识唯一的子 widget。`Global Keys` 在整个结构中心必须是全局唯一的，而不像 `Local Keys` 只需要在兄弟 widget 中唯一就行。

`When to use Keys`



# 资料

* [Flutter Widgets 101](https://www.youtube.com/playlist?list=PLOU2XLYxmsIJyiwUPCou_OVTpRIn_8UMd)