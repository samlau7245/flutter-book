
* `SliverSafeArea`:  SliverSafeArea的功能和SafeArea是一样的，区别就是SliverSafeArea用于Sliver控件
* `SliverAppBar`:  SliverAppBar控件可以实现页面头部区域展开、折叠的效果
 
* `SliverAnimatedList`: 动画
* `SliverAnimatedListState`: 动画
* `SliverAnimatedOpacity`: 动画
* `SliverFadeTransition`: 动画
 
* `SliverMultiBoxAdaptorElement`: 
* `SliverWithKeepAliveWidget`: 
	* `SliverMultiBoxAdaptorWidget`: 
		* `SliverGrid`:  要同时滚动ListView和GridView的时候可以使用SliverList和SliverGrid。
		* `SliverList`:  要同时滚动ListView和GridView的时候可以使用SliverList和SliverGrid。
		* `SliverFixedExtentList`:  和SliverList用法一样，唯一的区别就是SliverFixedExtentList是固定子控件的高度的，SliverFixedExtentList比SliverList更加高效
		* `SliverPrototypeExtentList`:  SliverList用法一样，区别是SliverPrototypeExtentList的高度由prototypeItem控件决定。
 
* `SliverOverlapAbsorber`: 
* `SliverOverlapAbsorberHandle`: 
* `SliverOverlapInjector`: 

* `SliverToBoxAdapter`: 使用CustomScrollView创建自定义滚动效果的时候，CustomScrollView只能包含sliver系列组件，如果包含普通的组件如何处理？使用SliverToBoxAdapter包裹。 
* `SliverFillRemaining`:  是sliver系列组件之一，此组件充满视口剩余空间，通常用于最后一个sliver组件，以便于没有任何剩余控件。
* `SliverFillViewport`:  SliverFillViewport生成的每一个item都占满全屏，

* `SliverPadding`: SliverPadding 组件是sliver系列的Padding组件，配合CustomScrollView使用。 比如给CustomScrollView中SliverList添加内边距：
* `SliverOffstage`:
* `SliverOpacity`: SliverOpacity是sliver系列组件，子控件为sliver组件，可设置子组件透明度，
* `SliverIgnorePointer`: 
* `SliverVisibility`: 

* `SliverPersistentHeader`:  控件当滚动到边缘时根据滚动的距离缩小高度，有点类似 SliverAppBar 的背景效果。
* `SliverPersistentHeaderDelegate`: 


* `SliverLayoutWidgetBuilder`: 
* `SliverLayoutBuilder`:  根据组件的约束条件提供子组件

* `SliverChildDelegate`: 
	* `SliverChildBuilderDelegate`: 
	* `SliverChildListDelegate`: 
* `SliverGridDelegate`: 
	* `SliverGridDelegateWithFixedCrossAxisCount`: 
	* `SliverGridDelegateWithMaxCrossAxisExtent`: 