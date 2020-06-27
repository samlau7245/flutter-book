
# 属性、方法

|属性|类型|说明|
| --- | --- | --- |
|currentIndex|int|当前索引|
|fixedColor|||
|iconColor|||
|items|`List<BtoomNavigationBarItem>`|底部导航栏按钮集合|
|onTap|`ValueChanged<int>`|按下其中某个按钮的回调事件。需要根据返回的索引设置当前索引|

> `type`控制项目的显示方式，如果没有指定，那么它会自动设置为`BottomNavigationBarType.fixed`. <br>
> `BottomNavigationBarType.fixed` : 当Items少于4个时，则会通过`selectedItemColor`显示选中Item的颜色，如果`selectedItemColor`为`null`，则使用`ThemeData.primaryColor`。如果`backgroundColor`为`null`，则使用`ThemeData.canvasColor`（本质上是不透明的白色）。<br>
> `BottomNavigationBarType.shifting` : 当Items大于等于4个时， 如果`selectedItemColor`为`null`，则所有项目均以白色呈现。背景颜色与所选项目的`BottomNavigationBarItem.backgroundColor`相同 。

* [代码示例1](https://codepen.io/samlau7245/pen/xxwabbb)
* [代码示例2,切换body为Scaffold](https://codepen.io/samlau7245/pen/JjYaGGY)

# 资料

* [flutter.dev-BottomNavigationBar Class](https://api.flutter.dev/flutter/material/BottomNavigationBar-class.html)