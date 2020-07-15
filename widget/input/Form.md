
[Form Class](https://api.flutter.dev/flutter/widgets/Form/Form.html)

# 构造函数

```dart
const Form({
  Key key,
  @required Widget child,
  bool autovalidate: false, // 是否自动校验输入内容
  WillPopCallback onWillPop,
  VoidCallback onChanged // Form中的内容发生变化的时候会触发此方法。
})
```

# 示例

```dart
class _FormExampleState extends State<FormExample> {
  @override
  Widget build(BuildContext context) {
    GlobalKey _formKey = new GlobalKey<FormState>();

    FocusNode focusNodeName = FocusNode();
    FocusNode focusNodePassword = FocusNode();

    return Scaffold(
      appBar: AppBar(
        title: Text("FormExample"),
      ),
      body: Padding(
        padding: const EdgeInsets.all(10.0),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                onEditingComplete: () {
                  focusNodePassword.requestFocus();
                },
                focusNode: focusNodeName,
                decoration: InputDecoration(
                  labelText: "用户名：",
                  icon: Icon(Icons.person),
                ),
                validator: (String value) {
                  return value.trim().length > 0 ? null : "用户名不能为空";
                },
              ),
              TextFormField(
                obscureText: true,
                focusNode: focusNodePassword,
                decoration: InputDecoration(
                  labelText: "密码：",
                  icon: Icon(Icons.lock),
                ),
                validator: (String value) {
                  return value.trim().length > 6 ? null : "密码不能少于6位";
                },
              ),
              Padding(
                padding: const EdgeInsets.only(top: 30.0),
                child: Row(
                  children: [
                    Expanded(
                      child: RaisedButton(
                        padding: EdgeInsets.all(15.0),
                        onPressed: () {
                          // 失去焦点，收起键盘。
                          focusNodeName.unfocus();
                          focusNodePassword.unfocus();

                          if ((_formKey.currentState as FormState).validate()) {
                            print("校验通过！");
                          }
                        },
                        child: Text("登录"),
                        textColor: Colors.white,
                        color: Theme.of(context).primaryColor,
                      ),
                    ),
                  ],
                ),
              )
            ],
          ),
        ),
      ),
    );
  }
}
```

<img src="/assets/images/widgets/28.png"/>

# [Form(表格)](https://api.flutter.dev/flutter/widgets/Form-class.html)

表格类，可以通过[Cookbook-Forms](https://flutter.dev/docs/cookbook/forms)来初步实现Form的创建；其中涉及到的Widget有：[FormField](https://api.flutter.dev/flutter/widgets/FormField-class.html)、[TextFormField](https://api.flutter.dev/flutter/material/TextFormField-class.html)、[DropdownButtonFormField](https://api.flutter.dev/flutter/material/DropdownButtonFormField-class.html)、[EditableText](https://api.flutter.dev/flutter/widgets/EditableText-class.html)、[InputDatePickerFormField](https://api.flutter.dev/flutter/material/InputDatePickerFormField-class.html)。

```dart
class TextFormField extends FormField<String>{}
class DropdownButtonFormField<T> extends FormField<T>{}
class EditableText extends StatefulWidget{}
```

[Form示例](https://codepen.io/samlau7245/pen/bGVxKXE)

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "FloatingActionButton Demo",
      home: HomePage(),
    );
  }
}

//////////////////////////////首页//////////////////////////////////

class HomePage extends StatefulWidget {
  HomePage({Key key}) : super(key: key);
  @override
  _HomePage createState() => new _HomePage();
}

class _HomePage extends State<HomePage> {
  // Create a global key that uniquely identifies the Form widget
  // and allows validation of the form.
  //
  // Note: This is a `GlobalKey<FormState>`,
  // not a GlobalKey<MyCustomFormState>.
  final _formKey = GlobalKey<FormState>();
  FocusNode _focusNode;
  List<String> _dropList;
  String _dropListSelected;
  final TextEditingController _controller = TextEditingController();

  @override
  void initState() {
    super.initState();
    _focusNode = FocusNode();
    _dropList = ["One", "Two"];
    _dropListSelected = _dropList.length <= 0 ? "" : _dropList.elementAt(0);
  }

  @override
  void dispose() {
    _focusNode.dispose();
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Demo")),
      body: Builder(
        builder: (BuildContext context) => Form(
          key: _formKey,
          child: Column(
            mainAxisAlignment: MainAxisAlignment.start,
            // Add TextFormFields and RaisedButton here.
            children: <Widget>[
              Padding(
                padding: const EdgeInsets.all(16.0),
                child: TextFormField(
                  //autofocus: true,
                  //focusNode: _focusNode,
                  decoration: const InputDecoration(
                    hintText: 'Enter your email',
                  ),
                  // 校验字段
                  validator: (value) {
                    if (value.isEmpty) {
                      return 'Please enter some text';
                    }
                    return null;
                  },
                  onChanged: (value) {
                    print(value);
                  },
                ),
              ),
              Padding(
                padding: EdgeInsets.only(left: 16.0, bottom: 16.0, right: 16.0),
                child: DropdownButtonFormField(
                  hint: const Text('Select Value'),
                  value: _dropListSelected,
                  items: _dropList
                      .map<DropdownMenuItem<String>>((String dropdownMenuItem) {
                    return DropdownMenuItem(
                      child: Text(dropdownMenuItem),
                      value: dropdownMenuItem,
                    );
                  }).toList(),
                  onChanged: (value) {},
                  validator: (String value) =>
                      value == null ? 'Must select value' : null,
                  onSaved: (String value) {
                    setState(() {
                      _dropListSelected = value;
                    });
                  },
                ),
              ),
              Padding(
                padding: EdgeInsets.only(left: 16.0, bottom: 16.0, right: 16.0),
                child: EditableText(
                  backgroundCursorColor: Colors.grey,
                  controller: _controller,
                  focusNode: _focusNode,
                  style: TextStyle(color: Colors.black),
                  cursorColor: Color.fromARGB(0xFF, 0xFF, 0x00, 0x00),
                ),
              ),
              InputDatePickerFormField(
                firstDate: DateTime(2018),
                lastDate: DateTime(2030),
              ),
              RaisedButton(
                onPressed: () {
                  if (_focusNode.canRequestFocus) {
                    _focusNode.requestFocus();
                  }
                  if (_formKey.currentState.validate()) {
                    Scaffold.of(context).showSnackBar(
                        SnackBar(content: Text('Processing Data')));
                  }
                },
                child: Text('Submit'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```