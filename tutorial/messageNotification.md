
可以在[极光文档](https://docs.jiguang.cn/jpush/client/client_plugins/)中找到Flutter插件。或者从`pub.dev`中找到[jpush_flutter](https://pub.dev/packages/jpush_flutter)插件。

<img src="/assets/images/tutorial/02.png"/>

极光推送的架构示意图：

<img src="/assets/images/tutorial/03.png"/>

# 添加依赖

```dart
# https://pub.dev/packages/jpush_flutter
dependencies:
  jpush_flutter: 0.5.5
```

# 项目配置

## Android配置

在 `/android/app/build.gradle` 中添加下列代码：

```gradle
defaultConfig {
    // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
    applicationId "com.example.proj_shop"
    
    manifestPlaceholders = [
    JPUSH_PKGNAME : applicationId,
    JPUSH_APPKEY : "appkey", // NOTE: JPush 上注册的包名对应的 Appkey.
    JPUSH_CHANNEL : "developer-default", //暂时填写默认值即可.
    ]
}
```

## iOS配置

在`XCode8`之后需要点开推送选项：`TARGETS -> Capabilities -> Push Notification` 设为`on`状态。

注意：要在开发者中把通知相关的证书、配置都配好。

<img src="/assets/images/tutorial/04.png"/>

<img src="/assets/images/tutorial/05.png"/>

# 极光配置

## 创建应用

<img src="/assets/images/tutorial/07.png"/>

## 上传证书

<img src="/assets/images/tutorial/06.png"/>

# 集成到代码

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  // This widget is the root of your application.
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  String debugLable = 'Unknown';
  final JPush jpush = new JPush();
  Future<void> initPlatformState() async {
    String platformVersion;
    try {
      jpush.addEventHandler(
        onReceiveNotification: (Map<String, dynamic> message) async {
          print("flutter onReceiveNotification: $message");
          setState(() {
            debugLable = "flutter onReceiveNotification: $message";
          });
        },
        onOpenNotification: (Map<String, dynamic> message) async {
          print("flutter onOpenNotification: $message");
          setState(() {
            debugLable = "flutter onOpenNotification: $message";
          });
        },
        onReceiveMessage: (Map<String, dynamic> message) async {
          print("flutter onReceiveMessage: $message");
          setState(() {
            debugLable = "flutter onReceiveMessage: $message";
          });
        },
        onReceiveNotificationAuthorization:
            (Map<String, dynamic> message) async {
          print("flutter onReceiveNotificationAuthorization: $message");
          setState(() {
            debugLable = "flutter onReceiveNotificationAuthorization: $message";
          });
        },
      );
    } on PlatformException {
      platformVersion = 'Failed to get platform version.';
    } catch (e) {}
    jpush.setup(
      appKey: '318094958c89512a1169bc13',
      channel: 'theChannel',
      production: false,
      debug: true,
    );
    jpush.applyPushAuthority(
      NotificationSettingsIOS(sound: true, alert: true, badge: true),
    );
    jpush.getRegistrationID().then((rid) {
      print("flutter get registration id : $rid");
      setState(() {
        debugLable = "flutter getRegistrationID: $rid";
      });
    });
    if (!mounted) {
      return;
    }
    setState(() {
      debugLable = platformVersion;
    });
  }

  @override
  void initState() {
    initPlatformState();
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: '百姓生活+',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(primaryColor: Colors.pink),
      //home: IndexPage(),
      home: Scaffold(
        appBar: AppBar(title: Text('Plugin example app')),
        body: Center(
          child: Column(
            children: [
              Container(
                margin: EdgeInsets.fromLTRB(10, 10, 10, 10),
                color: Colors.brown,
                child: Text(debugLable),
                width: 350,
                height: 100,
              ),
              Row(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: <Widget>[
                    new Text(" "),
                    new CustomButton(
                        title: "发本地推送",
                        onPressed: () {
                          // 三秒后出发本地推送
                          var fireDate = DateTime.fromMillisecondsSinceEpoch(
                              DateTime.now().millisecondsSinceEpoch + 3000);
                          var localNotification = LocalNotification(
                              id: 234,
                              title: 'fadsfa',
                              buildId: 1,
                              content: 'fdas',
                              fireTime: fireDate,
                              subtitle: 'fasf',
                              badge: 5,
                              extra: {"fa": "0"});
                          jpush
                              .sendLocalNotification(localNotification)
                              .then((res) {
                            setState(() {
                              debugLable = res;
                            });
                          });
                        }),
                    new Text(" "),
                    new CustomButton(
                        title: "getLaunchAppNotification",
                        onPressed: () {
                          jpush.getLaunchAppNotification().then((map) {
                            setState(() {
                              debugLable =
                                  "getLaunchAppNotification success: $map";
                            });
                          }).catchError((error) {
                            setState(() {
                              debugLable =
                                  "getLaunchAppNotification error: $error";
                            });
                          });
                        }),
                  ]),
              Row(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: <Widget>[
                    new Text(" "),
                    new CustomButton(
                        title: "setTags",
                        onPressed: () {
                          jpush.setTags(["lala", "haha"]).then((map) {
                            var tags = map['tags'];
                            setState(() {
                              debugLable = "set tags success: $map $tags";
                            });
                          }).catchError((error) {
                            setState(() {
                              debugLable = "set tags error: $error";
                            });
                          });
                        }),
                    new Text(" "),
                    new CustomButton(
                        title: "addTags",
                        onPressed: () {
                          jpush.addTags(["lala", "haha"]).then((map) {
                            var tags = map['tags'];
                            setState(() {
                              debugLable = "addTags success: $map $tags";
                            });
                          }).catchError((error) {
                            setState(() {
                              debugLable = "addTags error: $error";
                            });
                          });
                        }),
                    new Text(" "),
                    new CustomButton(
                        title: "deleteTags",
                        onPressed: () {
                          jpush.deleteTags(["lala", "haha"]).then((map) {
                            var tags = map['tags'];
                            setState(() {
                              debugLable = "deleteTags success: $map $tags";
                            });
                          }).catchError((error) {
                            setState(() {
                              debugLable = "deleteTags error: $error";
                            });
                          });
                        }),
                  ]),
              Row(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: <Widget>[
                    new Text(" "),
                    new CustomButton(
                        title: "getAllTags",
                        onPressed: () {
                          jpush.getAllTags().then((map) {
                            setState(() {
                              debugLable = "getAllTags success: $map";
                            });
                          }).catchError((error) {
                            setState(() {
                              debugLable = "getAllTags error: $error";
                            });
                          });
                        }),
                    new Text(" "),
                    new CustomButton(
                        title: "cleanTags",
                        onPressed: () {
                          jpush.cleanTags().then((map) {
                            var tags = map['tags'];
                            setState(() {
                              debugLable = "cleanTags success: $map $tags";
                            });
                          }).catchError((error) {
                            setState(() {
                              debugLable = "cleanTags error: $error";
                            });
                          });
                        }),
                  ]),
              Row(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: <Widget>[
                    new Text(" "),
                    new CustomButton(
                        title: "setAlias",
                        onPressed: () {
                          jpush.setAlias("thealias11").then((map) {
                            setState(() {
                              debugLable = "setAlias success: $map";
                            });
                          }).catchError((error) {
                            setState(() {
                              debugLable = "setAlias error: $error";
                            });
                          });
                        }),
                    new Text(" "),
                    new CustomButton(
                        title: "deleteAlias",
                        onPressed: () {
                          jpush.deleteAlias().then((map) {
                            setState(() {
                              debugLable = "deleteAlias success: $map";
                            });
                          }).catchError((error) {
                            setState(() {
                              debugLable = "deleteAlias error: $error";
                            });
                          });
                        }),
                  ]),
              Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  new Text(" "),
                  new CustomButton(
                      title: "stopPush",
                      onPressed: () {
                        jpush.stopPush();
                      }),
                  new Text(" "),
                  new CustomButton(
                      title: "resumePush",
                      onPressed: () {
                        jpush.resumePush();
                      }),
                ],
              ),
              Row(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: <Widget>[
                    new Text(" "),
                    new CustomButton(
                        title: "clearAllNotifications",
                        onPressed: () {
                          jpush.clearAllNotifications();
                        }),
                    new Text(" "),
                    new CustomButton(
                        title: "setBadge",
                        onPressed: () {
                          jpush.setBadge(66).then((map) {
                            setState(() {
                              debugLable = "setBadge success: $map";
                            });
                          }).catchError((error) {
                            setState(() {
                              debugLable = "setBadge error: $error";
                            });
                          });
                        }),
                  ]),
              Row(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: <Widget>[
                    new Text(" "),
                    new CustomButton(
                        title: "通知授权是否打开",
                        onPressed: () {
                          jpush.isNotificationEnabled().then((bool value) {
                            setState(() {
                              debugLable = "通知授权是否打开: $value";
                            });
                          }).catchError((onError) {
                            setState(() {
                              debugLable = "通知授权是否打开: ${onError.toString()}";
                            });
                          });
                        }),
                    new Text(" "),
                    new CustomButton(
                        title: "打开系统设置",
                        onPressed: () {
                          jpush.openSettingsForNotification();
                        }),
                  ]),
            ],
          ),
        ),
      ),
    );
  }
}

/// 封装控件
class CustomButton extends StatelessWidget {
  final VoidCallback onPressed;
  final String title;

  const CustomButton({@required this.onPressed, @required this.title});

  @override
  Widget build(BuildContext context) {
    return new FlatButton(
      onPressed: onPressed,
      child: new Text("$title"),
      color: Color(0xff585858),
      highlightColor: Color(0xff888888),
      splashColor: Color(0xff888888),
      textColor: Colors.white,
      //padding: EdgeInsets.fromLTRB(5, 5, 5, 5),
    );
  }
}
```

<img src="/assets/images/tutorial/08.png"/>

可以在官方中发推送消息[测试推送](https://www.jiguang.cn/jpush2/#/app/318094958c89512a1169bc13/push_form/notification)。

<img src="/assets/images/tutorial/09.png"/>

# 资料

* [掘金-Flutter应用集成极光推送](https://juejin.im/post/6844904073481682952)
* [Github-极光推送文档](https://github.com/jpush/jpush-flutter-plugin)