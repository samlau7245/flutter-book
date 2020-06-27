# [TextField(输入框)](https://api.flutter.dev/flutter/material/TextField-class.html)

* [TextFormField](https://api.flutter.dev/flutter/material/TextFormField-class.html)
* [Form](https://api.flutter.dev/flutter/widgets/Form-class.html)
* [可以从flutter 官方测试文件中找到Demo](https://github.com/flutter/flutter/blob/8de07d5527bcdc6b02e43e8efed19219a84bf82e/packages/flutter/test/material/text_field_test.dart)
* [使用TextEditingController](https://flutter.dev/docs/cookbook/forms/text-field-changes#2-use-a-texteditingcontroller)
* [CodePen示例](https://codepen.io/samlau7245/pen/QWjVmqM)

```dart
const TextField({
  Key key,
  this.controller, // 控制器
  this.focusNode,   // 轻按按钮时使文本字段聚焦,@see: https://flutter.dev/docs/cookbook/forms/focus                                             
  this.decoration = const InputDecoration(),//样式                                            
  TextInputType keyboardType,                                            
  this.textInputAction,                                            
  this.textCapitalization = TextCapitalization.none,                                            
  this.style, //类型                                            
  this.strutStyle,                                            
  this.textAlign = TextAlign.start,                                            
  this.textAlignVertical,                                            
  this.textDirection,                                            
  this.readOnly = false,                                            
  ToolbarOptions toolbarOptions,                                            
  this.showCursor,                                          // 光标设置                                            
  this.autofocus = false,     // 立即聚焦文本字段,@see: https://flutter.dev/docs/cookbook/forms/focus                                  
  this.obscureText = false,                                            
  this.autocorrect = true,                                            
  SmartDashesType smartDashesType,                                            
  SmartQuotesType smartQuotesType,                                            
  this.enableSuggestions = true,                                            
  this.maxLines = 1,// 行数限制                                           
  this.minLines,// 行数限制                                           
  this.expands = false,                                            
  this.maxLength,                                            
  this.maxLengthEnforced = true,                                            
  this.onChanged, // 输入监听回调                                            
  this.onEditingComplete, // 输入监听回调                                            
  this.onSubmitted, // 输入监听回调                                            
  this.inputFormatters,                                            
  this.enabled,                                            
  this.cursorWidth = 2.0,                                    // 光标设置
  this.cursorRadius,                                         // 光标设置
  this.cursorColor,                                          // 光标设置
  this.selectionHeightStyle = ui.BoxHeightStyle.tight,                                            
  this.selectionWidthStyle = ui.BoxWidthStyle.tight,                                            
  this.keyboardAppearance,                                            
  this.scrollPadding = const EdgeInsets.all(20.0),                                            
  this.dragStartBehavior = DragStartBehavior.start,                                            
  this.enableInteractiveSelection = true,                                            
  this.onTap,                                            
  this.buildCounter,                                            
  this.scrollController,                                            
  this.scrollPhysics,                                            
});

// 其中 `this.decoration = const InputDecoration()` 控制组件的样式，构造函数为：

const InputDecoration({
  this.icon,
  this.labelText,
  this.labelStyle,
  this.helperText,
  this.helperStyle,
  this.helperMaxLines,
  this.hintText,
  this.hintStyle,
  this.hintMaxLines,
  this.errorText,
  this.errorStyle,
  this.errorMaxLines,
  @Deprecated(
    'Use floatingLabelBehaviour instead. '
    'This feature was deprecated after v1.13.2.'
  )
  this.hasFloatingPlaceholder = true, // ignore: deprecated_member_use_from_same_package
  this.floatingLabelBehavior = FloatingLabelBehavior.auto,
  this.isDense,
  this.contentPadding,
  this.prefixIcon,
  this.prefixIconConstraints,
  this.prefix,
  this.prefixText,
  this.prefixStyle,
  this.suffixIcon,
  this.suffix,
  this.suffixText,
  this.suffixStyle,
  this.suffixIconConstraints,
  this.counter,
  this.counterText,
  this.counterStyle,
  this.filled,
  this.fillColor,
  this.focusColor,
  this.hoverColor,
  this.errorBorder,
  this.focusedBorder,
  this.focusedErrorBorder,
  this.disabledBorder,
  this.enabledBorder,
  this.border,
  this.enabled = true,
  this.semanticCounterText,
  this.alignLabelWithHint,
})
```