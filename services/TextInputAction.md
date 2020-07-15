
[TextInputAction Class](https://api.flutter.dev/flutter/services/TextInputAction-class.html)

```dart
enum TextInputAction {
  none,
  unspecified,//让操作系统决定哪个动作更合适
  done,//完成动作，一般会显示“完成”二字
  go,/// 跳转动作，一般用于输入了一个超链接后执行该动作。键盘上会显示“前往”二字
  search,//搜索动作
  send,//发送
  next,//下个
  previous,// 返回前一个
  continueAction,//继续动作
  join,
  route,
  emergencyCall,//拨打紧急电话
  newline, // 换行
}
```