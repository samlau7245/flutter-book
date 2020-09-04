
<img src="/assets/images/tutorial/10.png "/>

用到的依赖:

* `url_launcher`： 用于打开AppStore链接。

# 代码实现

```dart
class TutorialApp extends StatefulWidget {
  @override
  _TutorialAppState createState() => _TutorialAppState();
}

class _TutorialAppState extends State<TutorialApp> {

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      onGenerateRoute: generateRoute,
    );
  }
  Route generateRoute(RouteSettings routeSettings) {
    switch (routeSettings.name) {
      case '/page2':
        return MaterialPageRoute(builder: (_) => TutorialPage2());
      case '/page3':
        return MaterialPageRoute(builder: (_) => TutorialPage3());
      default:
        return MaterialPageRoute(builder: (_) => TutorialPage1());
    }
  }
}
```

主页面创建弹窗:

```dart
class TutorialPage1 extends StatefulWidget {
  @override
  _TutorialPage1State createState() => _TutorialPage1State();
}

class _TutorialPage1State extends State<TutorialPage1> {
  @override
  void initState() {
    updateAlert(context);
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold();
  }
}

Future<void> updateAlert(BuildContext context) async {
  Future.delayed(Duration(seconds: 2)).then((value) {
    // 显示升级弹窗
    showDialog(
      context: context,
      barrierDismissible: false, // 点击空白区域对话框不消失
      builder: (_) {
        return WillPopScope(
          child: TutorialUpdateDialog(),
          onWillPop: () {
            return;
          },
        );
      },
    );
  });
}
```

弹窗的Widget：

```dart
class TutorialUpdateDialog extends StatefulWidget {
  final bool isForceUpdate; // 是否强制更新

  const TutorialUpdateDialog({Key key, this.isForceUpdate = false})
      : super(key: key);
  @override
  _TutorialUpdateDialogState createState() => _TutorialUpdateDialogState();
}

class _TutorialUpdateDialogState extends State<TutorialUpdateDialog> {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Material(
        type: MaterialType.transparency,
        textStyle: TextStyle(color: Color(0xFF212121)),
        child: Container(
          width: MediaQuery.of(context).size.width * 0.8, // 宽度是整宽的百分之80
          decoration: BoxDecoration(
            color: Colors.white, // 背景白色
            borderRadius: BorderRadius.all(Radius.circular(4.0)), // 圆角
          ),
          child: Wrap(
            children: [
              SizedBox(height: 10, width: 20),
              // 关闭按钮
              Align(
                alignment: Alignment.topRight,
                child: widget.isForceUpdate
                    ? Container()
                    : InkWell(
                        onTap: () {
                          Navigator.pop(context);
                        },
                        child: Padding(
                          padding: const EdgeInsets.only(
                            top: 5.0,
                            right: 15.0,
                            bottom: 5.0,
                            left: 5.0,
                          ),
                          child: Icon(Icons.clear, color: Colors.black),
                        ),
                      ),
              ),
              // 模拟升级弹窗logo
              Center(child: FlutterLogo(size: 121.5)),
              // 升级到最新版本!
              Container(
                height: 30.0,
                width: double.infinity,
                alignment: Alignment.center,
                child: Text(
                  "升级到最新版本!",
                  style: TextStyle(
                    color: Color(0xff343243),
                    fontSize: 17.0,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              // 更新内容
              Container(
                width: double.infinity,
                alignment: Alignment.center,
                child: Padding(
                  padding: const EdgeInsets.symmetric(
                    horizontal: 40.0,
                    vertical: 15.0,
                  ),
                  child: Text(
                    "1. 修复了若干BUG!\n2. 程序员已经辞职！程序员已经辞职！程序员已经辞职！程序员已经辞职！",
                    style: TextStyle(
                      color: Color(0xff7A7A7A),
                    ),
                  ),
                ),
              ),
              // 立即升级
              Container(
                height: 80.0,
                width: double.infinity,
                padding: EdgeInsets.symmetric(horizontal: 10.0, vertical: 18.0),
                margin: EdgeInsets.only(bottom: 10.0),
                decoration: BoxDecoration(
                  borderRadius: BorderRadius.only(
                    bottomLeft: Radius.circular(12.0),
                    bottomRight: Radius.circular(12.0),
                  ),
                ),
                child: MaterialButton(
                  onPressed: () {
                    upgradeHandle();
                  },
                  child: Text("立即升级"),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }

  // 点击立即升级事件
  void upgradeHandle() {
    // 必须保证当前状态安全，才能进行状态刷新
    if (mounted) {
      setState(() {});
    }
    // 平台判断
    if (Platform.isAndroid) {
      _androidUpgrade();
    } else if (Platform.isIOS) {
      _iosUpgrade();
    }
  }

  // 安卓更新
  void _androidUpgrade() {}
  // iOS更新
  void _iosUpgrade() {
    _launchURL();
  }

  // 直接打开AppStore链接
  _launchURL() async {
    const url = "https://apps.apple.com/cn/app/%E5%BE%AE%E4%BF%A1/id414478124";
    if (await canLaunch(url)) {
      await launch(url);
    } else {
      throw 'Could not launch $url';
    }
  }
}
```