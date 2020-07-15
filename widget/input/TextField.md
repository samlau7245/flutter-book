
[TextField Class](https://api.flutter.dev/flutter/material/TextField-class.html)

# 构造函数

```dart
const TextField({
  Key key,
  TextEditingController controller, //编辑框的控制器，跟文本框的交互一般都通过该属性完成，如果不创建的话默认会自动创建
  FocusNode focusNode, //用于管理焦点
  InputDecoration decoration: const InputDecoration(),  //输入框的装饰器，用来修改外观
  TextInputType keyboardType, //设置输入类型，不同的输入类型键盘不一样
  TextInputAction textInputAction, //用于控制键盘动作（一般位于右下角，默认是完成）
  TextCapitalization textCapitalization: TextCapitalization.none, // 键盘输入字符大小写
  TextStyle style, //输入的文本样式
  StrutStyle strutStyle,
  TextAlign textAlign: TextAlign.start,  //输入的文本位置
  TextAlignVertical textAlignVertical,
  TextDirection textDirection, //输入的文字排列方向，一般不会修改这个属性
  bool readOnly: false,
  ToolbarOptions toolbarOptions,
  bool showCursor,
  bool autofocus: false, //是否自动获取焦点
  bool obscureText: false, //是否隐藏输入的文字，一般用在密码输入框中
  bool autocorrect: true,  //是否自动校验
  SmartDashesType smartDashesType,
  SmartQuotesType smartQuotesType,
  bool enableSuggestions: true,
  int maxLines: 1, //最大行
  int minLines,
  bool expands: false,
  int maxLength,  //能输入的最大字符个数
  bool maxLengthEnforced: true, //配合maxLength一起使用，在达到最大长度时是否阻止输入
  ValueChanged<String> onChanged, //输入文本发生变化时的回调
  VoidCallback onEditingComplete, //点击键盘完成按钮时触发的回调，该回调没有参数，(){}
  ValueChanged<String> onSubmitted,  //同样是点击键盘完成按钮时触发的回调，该回调有参数，参数即为当前输入框中的值。(String){}
  List<TextInputFormatter> inputFormatters, //对输入文本的校验
  bool enabled, //输入框是否可用
  double cursorWidth: 2.0, //光标的宽度
  Radius cursorRadius, //光标的圆角
  Color cursorColor, //光标的颜色
  BoxHeightStyle selectionHeightStyle: ui.BoxHeightStyle.tight,
  BoxWidthStyle selectionWidthStyle: ui.BoxWidthStyle.tight,
  Brightness keyboardAppearance,
  EdgeInsets scrollPadding: const EdgeInsets.all(20.0),
  DragStartBehavior dragStartBehavior: DragStartBehavior.start,
  bool enableInteractiveSelection: true,
  GestureTapCallback onTap, //点击输入框时的回调
  InputCounterWidgetBuilder buildCounter,
  ScrollController scrollController,
  ScrollPhysics scrollPhysics
})
```

# 示例

## 给 TextField 添加颜色

```dart
Theme(
  data: ThemeData(
    primaryColor: Colors.red,
    hintColor: Colors.green,
  ),
  child: TextField(
    controller: textEditingController,
    decoration: InputDecoration(
      labelText: 'Hello',
    ),
  ),
)
```

<img src="/assets/images/widgets/25.png"/>

# 资料

* [TextFormField](https://api.flutter.dev/flutter/material/TextFormField-class.html)
* [Form](https://api.flutter.dev/flutter/widgets/Form-class.html)
* [可以从flutter 官方测试文件中找到Demo](https://github.com/flutter/flutter/blob/8de07d5527bcdc6b02e43e8efed19219a84bf82e/packages/flutter/test/material/text_field_test.dart)
* [使用TextEditingController](https://flutter.dev/docs/cookbook/forms/text-field-changes#2-use-a-texteditingcontroller)
* [CodePen示例](https://codepen.io/samlau7245/pen/QWjVmqM)


























