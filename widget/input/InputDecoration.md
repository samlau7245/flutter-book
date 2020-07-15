
[InputDecoration Class](https://api.flutter.dev/flutter/material/InputDecoration-class.html)

# 构造函数

## InputDecoration()

```dart
const InputDecoration({
	Widget icon, //位于装饰器外部和输入框前面的图片
	
	String labelText, //用于描述输入框，例如这个输入框是用来输入用户名还是密码的，当输入框获取焦点时默认会浮动到上方，
	TextStyle labelStyle, // 控制labelText的样式,接收一个TextStyle类型的值
	String helperText, //辅助文本，位于输入框下方，如果errorText不为空的话，则helperText不会显示
	TextStyle helperStyle,//helperText的样式
	int helperMaxLines, 
	String hintText, //提示文本，位于输入框内部
	TextStyle hintStyle, //hintText的样式
	int hintMaxLines,
	String errorText, //错误信息提示
	TextStyle errorStyle, //errorText的样式
	int errorMaxLines,

	@Deprecated('Use floatingLabelBehaviour instead. ' 'This feature was deprecated after v1.13.2.') bool hasFloatingPlaceholder: true,//labelText是否浮动，默认为true，修改为false则labelText在输入框获取焦点时不会浮动且不显示
	FloatingLabelBehavior floatingLabelBehavior: FloatingLabelBehavior.auto,
	bool isDense,//改变输入框是否为密集型，默认为false，修改为true时，图标及间距会变小
	EdgeInsetsGeometry contentPadding,//内间距
	
	Widget prefixIcon, //位于输入框内部起始位置的图标。
	BoxConstraints prefixIconConstraints,
	Widget prefix,//预先填充的Widget,跟prefixText同时只能出现一个
	String prefixText,//预填充的文本，例如手机号前面预先加上区号等
	TextStyle prefixStyle,//prefixText的样式
	
	Widget suffixIcon,  //位于输入框后面的图片,例如一般输入框后面会有个眼睛，控制输入内容是否明文
	Widget suffix,   //位于输入框尾部的控件，同样的不能和suffixText同时使用
	String suffixText, //位于尾部的填充文字
	TextStyle suffixStyle,//suffixText的样式
	BoxConstraints suffixIconConstraints,
	
	Widget counter, //位于输入框右下方的小控件，不能和counterText同时使用
	String counterText, //位于右下方显示的文本，常用于显示输入的字符数量
	TextStyle counterStyle,  //counterText的样式
	
	bool filled, //如果为true，则输入使用fillColor指定的颜色填充
	Color fillColor, //相当于输入框的背景颜色
	Color focusColor,
	Color hoverColor,
	
	InputBorder errorBorder,//errorText不为空，输入框没有焦点时要显示的边框
	InputBorder focusedBorder,//输入框有焦点时的边框,如果errorText不为空的话，该属性无效
	InputBorder focusedErrorBorder, //errorText不为空时，输入框有焦点时的边框
	InputBorder disabledBorder,   //输入框禁用时显示的边框，如果errorText不为空的话，该属性无效
	InputBorder enabledBorder,   //输入框可用时显示的边框，如果errorText不为空的话，该属性无效
	InputBorder border,  //正常情况下的border
	
	bool enabled: true,  //输入框是否可用
	String semanticCounterText,
	bool alignLabelWithHint
})
```

## InputDecoration.collapsed()

```dart
const InputDecoration.collapsed({
	@required String hintText,
	@Deprecated('Use floatingLabelBehaviour instead. ' 'This feature was deprecated after v1.13.2.') bool hasFloatingPlaceholder: true,
	FloatingLabelBehavior floatingLabelBehavior: FloatingLabelBehavior.auto,
	TextStyle hintStyle,
	bool filled: false,
	Color fillColor,
	Color focusColor,
	Color hoverColor,
	InputBorder border: InputBorder.none,
	bool enabled: true
})
```

# 示例

```dart
TextField(
  decoration: InputDecoration(
    icon: Icon(Icons.add),
    labelText: "labelText",
    helperText: "helperText",
    hintText: "helperText",
    errorText: "errorText",
  ),
)
```
<img src="/assets/images/widgets/18.png"/>

```dart
TextField(
  decoration: InputDecoration(
    icon: Icon(Icons.add),
    labelText: "labelText",
    helperText: "helperText",
    hintText: "hintText",
    errorText: "errorText",
  ),
)
```
<img src="/assets/images/widgets/18.png"/>

```dart
TextField(
  decoration: InputDecoration(
    icon: Icon(Icons.add),
    labelText: "labelText",
    helperText: "helperText",
    hintText: "hintText",
    // errorText: "errorText",
  ),
)
```
<img src="/assets/images/widgets/19.png"/>

```dart
TextField(
  controller: textEditingController,
  decoration: InputDecoration(
    prefixText: "prefixText",
    suffixText: "suffixText",
  ),
)
```
<img src="/assets/images/widgets/20.png"/>

```dart
TextField(
  controller: textEditingController,
  decoration: InputDecoration(
    prefixText: "prefixText",
    suffixText: "suffixText",
    contentPadding: EdgeInsets.all(15.0),
  ),
)
```
<img src="/assets/images/widgets/21.png"/>

```dart
TextField(
  controller: textEditingController,
  decoration: InputDecoration(
    fillColor: Colors.blue.shade100,
    filled: true,
    labelText: 'Hello',
  ),
)
```
<img src="/assets/images/widgets/22.png"/>

```dart
TextField(
  controller: textEditingController,
  decoration: InputDecoration(
    labelText: 'Hello',
    prefixIcon: Icon(Icons.phone),
    suffixIcon: Icon(Icons.offline_bolt),
  ),
)
```
<img src="/assets/images/widgets/23.png"/>

```dart
TextField(
  controller: textEditingController,
  decoration: InputDecoration(
    labelText: 'Hello',
    prefixIcon: Icon(Icons.phone),
    suffixIcon: Icon(Icons.offline_bolt),
    border: OutlineInputBorder(
      borderRadius: BorderRadius.circular(15.0),
    ),
  ),
)
```

<img src="/assets/images/widgets/24.png"/>