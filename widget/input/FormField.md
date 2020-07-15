
[FormField Class](https://api.flutter.dev/flutter/widgets/FormField-class.html)

# 构造函数

```dart
const FormField<T>({
	Key key,
	@required FormFieldBuilder<T> builder,
	FormFieldSetter<T> onSaved, //保存时触发
	FormFieldValidator<T> validator, //验证时触发
	T initialValue, //初始化值
	bool autovalidate: false, //是否自动校验
	bool enabled: true
})
```

# 自定义 FormField

实现一个demo，用户输入姓名、年纪，并且进行打印：

<img src="/assets/images/widgets/29.png"/>

```
class _FormFieldExampleState extends State<FormFieldExample> {
  final _formKey = GlobalKey<FormState>();
  String name;
  int age;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("FormFieldExample"),
      ),
      body: Center(
        child: Form(
          key: this._formKey,
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              Text('Please fill in your name and age'),
              TextFormField(
                autovalidate: false,
                onSaved: (value) => this.name = value,
                validator: (value) {
                  return value.length < 3
                      ? 'a minimum of 3 characters is required'
                      : null;
                },
              ),
              Counter(),
              RaisedButton(
                child: Text('Submit'),
                onPressed: () {
                  if (this._formKey.currentState.validate()) {
                    setState(() {
                      this._formKey.currentState.save();
                    });
                  }
                },
              ),
              SizedBox(height: 50.0),
              Text('${this.name} is ${this.age} years old')
            ],
          ),
        ),
      ),
    );
  }
}
```

其中`Counter()`为计数的自定义Widget:

```dart
class Counter extends StatefulWidget {
  @override
  _CounterState createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int value;

  @override
  void initState() {
    this.value = 0;
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisSize: MainAxisSize.min,
      children: [
        IconButton(
          icon: Icon(Icons.remove),
          onPressed: () {
            setState(() {
              if (this.value > 0) {
                this.value--;
              }
            });
          },
        ),
        Padding(
          padding: const EdgeInsets.only(left: 20.0, right: 20.0),
          child: Text(this.value.toString()),
        ),
        IconButton(
          icon: Icon(Icons.add),
          onPressed: () {
            setState(() {
              this.value++;
            });
          },
        )
      ],
    );
  }
}
```

现在如果把`Counter()`做成成像`FormField`一样的表单输入，可以通过继承`FormField`完成：

```dart
class CounterFieldExample extends FormField<int> {
  CounterFieldExample(
      {FormFieldSetter<int> onSaved,
      FormFieldValidator<int> validator,
      int initialValue = 0,
      bool autovalidate: false,
      bool enabled: true})
      : super(
            onSaved: onSaved,
            validator: validator,
            initialValue: initialValue,
            autovalidate: autovalidate,
            builder: (FormFieldState<int> field) {
              return Column(
                children: [
                  // Counter 计数器Widget
                  Row(
                    mainAxisSize: MainAxisSize.min,
                    children: [
                      IconButton(
                        icon: Icon(Icons.remove),
                        onPressed: () {
                          field.didChange(field.value - 1);
                          print("remove ${field.value}");
                        },
                      ),
                      Padding(
                        padding: const EdgeInsets.only(left: 20.0, right: 20.0),
                        child: Text(field.value.toString()),
                      ),
                      IconButton(
                        icon: Icon(Icons.add),
                        onPressed: () {
                          field.didChange(field.value + 1);
                          print("add ${field.value}");
                        },
                      )
                    ],
                  ),
                  // 添加错误提示
                  field.hasError
                      ? Text(
                          field.errorText,
                          style: TextStyle(color: Colors.red),
                        )
                      : Container()
                ],
              );
            });
}
```

现在集成`CounterFieldExample`：

```dart
CounterFieldExample(
  autovalidate: false,
  onSaved: (value) => this.age = value,
  validator: (int value) {
    print(value);
    return value < 0 ? 'Negative values not supported' : null;
  },
),
```

<img src="/assets/images/widgets/30.png"/>