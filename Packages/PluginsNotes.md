# 官方维护的插件

|插件|功能|平台|
| --- | --- | --- |
|[android_alarm_manager](https://github.com/flutter/plugins/tree/master/packages/android_alarm_manager)| | |
|[android_intent](https://github.com/flutter/plugins/tree/master/packages/android_intent)| | |
|[battery](https://github.com/flutter/plugins/tree/master/packages/battery)| | |
|[camera](https://github.com/flutter/plugins/tree/master/packages/camera)| | |
|[connectivity](https://github.com/flutter/plugins/tree/master/packages/connectivity)| | |
|[device_info](https://github.com/flutter/plugins/tree/master/packages/device_info)| | |
|[e2e](https://github.com/flutter/plugins/tree/master/packages/e2e)| | |
|[espresso](https://github.com/flutter/plugins/tree/master/packages/espresso)| | |
|[flutter_plugin_android_lifecycle](https://github.com/flutter/plugins/tree/master/packages/flutter_plugin_android_lifecycle)| | |
|[google_maps_flutter](https://github.com/flutter/plugins/tree/master/packages/google_maps_flutter)| | |
|[google_sign_in](https://github.com/flutter/plugins/tree/master/packages/google_sign_in)| | |
|[image_picker](https://github.com/flutter/plugins/tree/master/packages/image_picker)| | |
|[in_app_purchase](https://github.com/flutter/plugins/tree/master/packages/in_app_purchase)| | |
|[ios_platform_images](https://github.com/flutter/plugins/tree/master/packages/ios_platform_images)| | |
|[local_auth](https://github.com/flutter/plugins/tree/master/packages/local_auth)| | |
|[package_info](https://github.com/flutter/plugins/tree/master/packages/package_info)| 获取package的信息| |
|[path_provider](https://github.com/flutter/plugins/tree/master/packages/path_provider)| | |
|[plugin_platform_interface](https://github.com/flutter/plugins/tree/master/packages/plugin_platform_interface)| | |
|[quick_actions](https://github.com/flutter/plugins/tree/master/packages/quick_actions)| | |
|[sensors](https://github.com/flutter/plugins/tree/master/packages/sensors)| | |
|[share](https://github.com/flutter/plugins/tree/master/packages/share)| | |
|[shared_preferences](https://github.com/flutter/plugins/tree/master/packages/shared_preferences)| | |
|[url_launcher](https://github.com/flutter/plugins/tree/master/packages/url_launcher)| | |
|[video_player](https://github.com/flutter/plugins/tree/master/packages/video_player)| |ANDROID、IOS|
|[webview_flutter](https://github.com/flutter/plugins/tree/master/packages/webview_flutter)| | |
|[provider](https://pub.dev/packages/provider)| 状态管理 | ANDROID、IOS、WEB |

# 非官方
|插件|功能|平台|
| --- | --- | --- |
| [SQLite](https://pub.flutter-io.cn/packages/sqflite) |SQLite|ANDROID、IOS|
| [flutter_datetime_picker](https://pub.flutter-io.cn/packages/flutter_datetime_picker) | 时间选择器|ANDROID、IOS、WEB|
| [flutter_webview_plugin](https://pub.dev/packages/flutter_webview_plugin) | 网页组件 |ANDROID、IOS|
| [flutter_screenutil](https://pub.dev/packages/flutter_screenutil) | 屏幕适配 |ANDROID、IOS、WEB|
| [fluttertoast](https://pub.dev/packages/fluttertoast) | toast |ANDROID、IOS|

# provider

* [YouTube-使用示例](https://www.youtube.com/watch?v=rfAzMf_Z2Rs)

# webview_flutter

## 基础

在iOS中添加配置:

```xml
<key>io.flutter.embedded_views_preview</key>
<string>YES</string>
```

## 代码

```dart
const WebView({
  Key key,
  WebViewCreatedCallback onWebViewCreated, // WebView创建完成时调用
  this.initialUrl, // 需要加载的链接URL
  this.javascriptMode = JavascriptMode.disabled, // JS执行模式
  this.javascriptChannels, // 使用javascriptChannel JS可以调用Flutter
  NavigationDelegate navigationDelegate, // 拦截请求
  this.gestureRecognizers, // 手势
  this.onPageStarted,
  this.onPageFinished, // 页面加载完成
  this.onWebResourceError,
  this.debuggingEnabled = false,
  this.gestureNavigationEnabled = false,
  this.userAgent,
  this.initialMediaPlaybackPolicy = AutoMediaPlaybackPolicy.require_user_action_for_all_media_types,
})
```

`navigationDelegate`：

```dart
WebView(
  navigationDelegate: (NavigationRequest navigation) {
    return NavigationDecision.navigate;
  },
),

enum NavigationDecision {
  prevent, // 需要执行拦截
  navigate, // 不需要拦截操作 
}
```

## 完整代码

```dart
class _MemberPageState extends State<MemberPage> {
  WebViewController _webViewController;
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('会员中心')),
      body: WebView(
        initialUrl: 'http://192.168.20.40:4011/web.html',
        javascriptMode: JavascriptMode.unrestricted,
        onWebViewCreated: (WebViewController webViewController) {
          _webViewController = webViewController;
        },
        onPageFinished: (String url) {
          /*String javascriptString = "window.isLogin=是否登录";
           _webViewController
              .evaluateJavascript(javascriptString)
              .then((value) {});*/
        },
        onPageStarted: (String url) {},
        navigationDelegate: (NavigationRequest navigation) {
          print(navigation.url);
          // //不需要拦截的操作
          return NavigationDecision.navigate;
        },
        gestureNavigationEnabled: true,
        userAgent: "uhome",
      ),
    );
  }
}
```

# flutter_webview_plugin

## 配置

iOS：

```xml
<key>NSAppTransportSecurity</key>
<dict>
	<key>NSAllowsArbitraryLoads</key>
	<true/>
	<key>NSAllowsArbitraryLoadsInWebContent</key>
<true/>
</dict>
```

## 代码解析

```dart
const WebviewScaffold({
  Key key,
  PreferredSizeWidget appBar,
  String url, // 网页链接
  Map<String, String> headers,
  Set<JavascriptChannel> javascriptChannels,
  bool withJavascript,
  bool clearCache,
  bool clearCookies,
  bool mediaPlaybackRequiresUserGesture = true,
  bool enableAppScheme,
  String userAgent,
  bool primary = true,
  List<Widget> persistentFooterButtons,
  Widget bottomNavigationBar,
  bool withZoom,
  bool displayZoomControls,
  bool withLocalStorage,
  bool withLocalUrl,
  String localUrlScope,
  bool withOverviewMode,
  bool useWideViewPort,
  bool scrollBar,
  bool supportMultipleWindows,
  Widget appCacheEnabled,
  bool hidden = false,
  bool initialChild,
  String allowFileURLs,
  bool resizeToAvoidBottomInset = false,
  bool invalidUrlRegex,
  bool geolocationEnabled,
  bool debuggingEnabled = false,
  bool ignoreSSLErrors = false,
})
```

## 完整代码

```dart
class _MemberPageState extends State<MemberPage> {
  @override
  Widget build(BuildContext context) {
    return WebviewScaffold(
      appBar: AppBar(title: Text("会员中心")),
      url: 'http://192.168.20.40:4011/web.html',
      withZoom: true,
      withLocalStorage: true,
      hidden: true,
      initialChild: Container(
        color: Colors.redAccent,
        child: const Center(
          child: Text('Waiting.....'),
        ),
      ),
    );
  }
}
```

# 资料
* [https://juejin.im/post/5de48586e51d455c0172baac](https://juejin.im/post/5de48586e51d455c0172baac)