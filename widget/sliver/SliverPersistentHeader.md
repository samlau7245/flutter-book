
* [SliverPersistentHeader-class](https://api.flutter.dev/flutter/widgets/SliverPersistentHeader-class.html)
* [SliverPersistentHeaderDelegate-class](https://api.flutter.dev/flutter/widgets/SliverPersistentHeaderDelegate-class.html)

# 构造函数

```dart
SliverPersistentHeader({
	Key key, 
	@required SliverPersistentHeaderDelegate delegate, // 需要创建其子类实现功能
	bool pinned: false, 
	bool floating: false
})
```

## SliverPersistentHeaderDelegate

```dart
class MySliverPersistentHeaderDelegate extends SliverPersistentHeaderDelegate {
  // 构建渲染的内容
  @override
  Widget build(
      BuildContext context, double shrinkOffset, bool overlapsContent) {
    throw UnimplementedError();
  }

  @override
  double get maxExtent => throw UnimplementedError(); // 展开状态下组件的高度

  @override
  double get minExtent => throw UnimplementedError(); // 收起状态下组件的高度

  // 更新组件
  @override
  bool shouldRebuild(SliverPersistentHeaderDelegate oldDelegate) {
    throw UnimplementedError();
  }
}
```

# 示例

## 构建吸顶效果

实现代理方法：

```dart
class MySliverPersistentHeaderDelegate extends SliverPersistentHeaderDelegate {
  final TabBar child;

  MySliverPersistentHeaderDelegate({@required this.child});

  // 构建渲染的内容
  @override
  Widget build(
      BuildContext context, double shrinkOffset, bool overlapsContent) {
    return this.child;
  }

  @override
  double get maxExtent => this.child.preferredSize.height; // 展开状态下组件的高度

  @override
  double get minExtent => this.child.preferredSize.height; // 收起状态下组件的高度

  // 更新组件
  @override
  bool shouldRebuild(SliverPersistentHeaderDelegate oldDelegate) {
    return true;
  }
}
```

实现功能：

```dart
class StickyTabBarDemo extends StatefulWidget {
  @override
  _StickyTabBarDemoState createState() => _StickyTabBarDemoState();
}

class _StickyTabBarDemoState extends State<StickyTabBarDemo>
    with SingleTickerProviderStateMixin {
  TabController tabController;
  @override
  void initState() {
    this.tabController = TabController(length: 2, vsync: this);
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: CustomScrollView(
        slivers: [
          SliverAppBar(
            pinned: true,
            expandedHeight: 250,
            elevation: 0.0,
            flexibleSpace: FlexibleSpaceBar(
              title: Text("SliverAppBar"),
              background: Image.network(
                'http://img1.mukewang.com/5c18cf540001ac8206000338.jpg',
                fit: BoxFit.cover,
              ),
            ),
          ),
          SliverPersistentHeader(
            pinned: true,
            delegate: MySliverPersistentHeaderDelegate(
              child: TabBar(
                labelColor: Colors.black,
                controller: this.tabController,
                tabs: [
                  Tab(text: 'Home'),
                  Tab(text: 'Profile'),
                ],
              ),
            ),
          ),
          SliverFillRemaining(
            child: TabBarView(
              controller: this.tabController,
              children: <Widget>[
                Center(child: Text('Content of Home')),
                Center(child: Text('Content of Profile')),
              ],
            ),
          ),
        ],
      ),
    );
  }
}
```

<img src="/assets/images/widgets/53.gif"/>


## 下拉图片方法

先上效果：

<img src="/assets/images/widgets/55.gif"/>

组件实现：

```dart
class BackImageZoomDemo extends StatefulWidget {
  @override
  _BackImageZoomDemoState createState() => _BackImageZoomDemoState();
}

class _BackImageZoomDemoState extends State<BackImageZoomDemo> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: CustomScrollView(
        slivers: [
          SliverPersistentHeader(
            pinned: true,
            delegate: BackImageZoomHeaderDelegate(
                title: '哪吒之魔童降世',
                collapsedHeight: 40,
                expandedHeight: 300,
                paddingTop: MediaQuery.of(context).padding.top,
                coverImgUrl:
                    'https://img.zcool.cn/community/01c6615d3ae047a8012187f447cfef.jpg@1280w_1l_2o_100sh.jpg'),
          ),
          SliverFillRemaining(
            child: ContentWidget(),
          )
        ],
      ),
    );
  }
}
```

实现Header的代理：

```dart
class BackImageZoomHeaderDelegate extends SliverPersistentHeaderDelegate {
  final double collapsedHeight;
  final double expandedHeight;
  final double paddingTop;
  final String coverImgUrl;
  final String title;
  String statusBarMode = 'dark';

  BackImageZoomHeaderDelegate(
      {this.collapsedHeight,
      this.expandedHeight,
      this.paddingTop,
      this.coverImgUrl,
      this.title});

  @override
  Widget build(
      BuildContext context, double shrinkOffset, bool overlapsContent) {
    return Container(
      height: this.maxExtent,
      width: MediaQuery.of(context).size.width,
      child: Stack(
        fit: StackFit.expand,
        children: <Widget>[
          Container(child: Image.network(this.coverImgUrl, fit: BoxFit.cover)),
          Positioned(
            left: 0,
            top: this.maxExtent / 2,
            right: 0,
            bottom: 0,
            child: Container(
              decoration: BoxDecoration(
                gradient: LinearGradient(
                  begin: Alignment.topCenter,
                  end: Alignment.bottomCenter,
                  colors: [
                    Color(0x00000000),
                    Color(0x90000000),
                  ],
                ),
              ),
            ),
          ),
          Positioned(
            left: 0,
            right: 0,
            top: 0,
            child: Container(
              color: this.makeStickyHeaderBgColor(shrinkOffset),
              child: SafeArea(
                bottom: false,
                child: Container(
                  height: this.collapsedHeight,
                  child: Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: <Widget>[
                      IconButton(
                        icon: Icon(
                          Icons.arrow_back_ios,
                          color: this
                              .makeStickyHeaderTextColor(shrinkOffset, true),
                        ),
                        onPressed: () => Navigator.pop(context),
                      ),
                      Text(
                        this.title,
                        style: TextStyle(
                          fontSize: 20,
                          fontWeight: FontWeight.w500,
                          color: this
                              .makeStickyHeaderTextColor(shrinkOffset, false),
                        ),
                      ),
                      IconButton(
                        icon: Icon(
                          Icons.share,
                          color: this
                              .makeStickyHeaderTextColor(shrinkOffset, true),
                        ),
                        onPressed: () {},
                      ),
                    ],
                  ),
                ),
              ),
            ),
          ),
        ],
      ),
    );
  }
```



正文内容:

```dart
class ContentWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(8.0),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Row(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              ClipRRect(
                borderRadius: BorderRadius.circular(6),
                child: Image.network(
                  "https://img1.gamersky.com/image2019/07/20190725_ll_red_136_2/gamersky_07small_14_201972510258D0.jpg",
                  width: 130,
                  height: 180,
                  fit: BoxFit.cover,
                ),
              ),
              Padding(
                padding: const EdgeInsets.only(left: 16),
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text(
                      "哪吒之魔童降世",
                      style: TextStyle(
                        fontSize: 25,
                        fontWeight: FontWeight.bold,
                        color: Color(0xFF333333),
                      ),
                    ),
                    Padding(
                      padding: const EdgeInsets.only(top: 10),
                      child: Text(
                        '动画/中国大陆/110分钟',
                        style: TextStyle(
                          fontSize: 15,
                          color: Color(0xFF999999),
                        ),
                      ),
                    ),
                    Padding(
                      padding: EdgeInsets.only(top: 2),
                      child: Text(
                        '2019-07-26 08:00 中国大陆上映',
                        style: TextStyle(
                          fontSize: 15,
                          color: Color(0xFF999999),
                        ),
                      ),
                    ),
                    Padding(
                      padding: EdgeInsets.only(top: 2),
                      child: Text(
                        '32.1万人想看/大V推荐度95%',
                        style: TextStyle(
                          fontSize: 15,
                          color: Color(0xFF999999),
                        ),
                      ),
                    ),
                  ],
                ),
              ),
            ],
          ),
          Divider(height: 32),
          Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Text(
                '剧情简介',
                style: TextStyle(
                  fontSize: 25,
                  fontWeight: FontWeight.bold,
                  color: Color(0xFF333333),
                ),
              ),
              Padding(
                padding: const EdgeInsets.only(top: 10),
                child: Text(
                  '天地灵气孕育出一颗能量巨大的混元珠，元始天尊将混元珠提炼成灵珠和魔丸，灵珠投胎为人，助周伐纣时可堪大用；而魔丸则会诞出魔王，为祸人间。元始天尊启动了天劫咒语，3年后天雷将会降临，摧毁魔丸。太乙受命将灵珠托生于陈塘关李靖家的儿子哪吒身上。然而阴差阳错，灵珠和魔丸竟然被掉包。本应是灵珠英雄的哪吒却成了混世大魔王。调皮捣蛋顽劣不堪的哪吒却徒有一颗做英雄的心。然而面对众人对魔丸的误解和即将来临的天雷的降临，哪吒是否命中注定会立地成魔？他将何去何从？',
                  textAlign: TextAlign.justify,
                  style: TextStyle(
                    fontSize: 15,
                    color: Color(0xFF999999),
                  ),
                ),
              ),
            ],
          ),
        ],
      ),
    );
  }
}
```