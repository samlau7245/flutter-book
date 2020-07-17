
# 函数

在Dart中，函数也是一种对象，有拥有类型[Function](https://api.dartlang.org/stable/dart-core/Function-class.html)。 这也意味着函数可以被赋值给变量或者作为参数传递给其他函数。

`=> expr` 语法是 `{ return expr; }` 的简写。 `=>` 符号 有时也被称为 `箭头` 语法。

> **[warning] 提示**
>
> 在箭头 (=>) 和分号 (;) 之间只能使用一个 表达式 ，不能是 语句 。 

# 函数参数

## optional 可选参数

```dart
Function funcA(num var1,num var2) => (){ return var1 + var2;}; // 参数不可缺少
Function funcB({num var1,num var2}) => (){ return var1 + var2;}; // 参数可选

void main() {
  funcA(1,2);
  funcB(var1:1);
}
```

## required 必选参数

```dart
Function funcC({num var1,@required num var2}) => (){ return var1 + var2;}; // var2参数必须传入。

void main() {
  funcB(var2:1);
}
```

## 位置可选参数

将参数放到 `[]` 中来标记参数是可选的

```dart
Function funcC(num var1,num var2,[num var3]) => (){ return var1 + var2 + var3;};
void main() {
  funcB(1,2);
  funcB(1,2,3);
}
```

## 默认参数值

使用 `=` 来定义可选参数的默认值。如果没有提供默认值，则默认值为 `null`。

```dart
void enableFlags({bool bold = false, bool hidden = false}){}
```

# 匿名函数

匿名函数 : 没有名字的函数。有时候也被称为 `lambda` 或者 `closure` 。

```dart
list.forEach(
    (item) => print('${list.indexOf(item)}: $item') // 这就是个典型的匿名函数
);
```

## 匿名函数作为函数参数

```dart
// 无入参，无返回值
void blockA(void Function() block) {
  block();
}

// 无入参，有返回值
void blockB(void Function(int arg1, int arg2) block) {
  block(1, 2);
}

// 有入参，有返回值
void blockC(int Function(int arg1, int arg2) block) {
  int ret = block(1, 2);
  print("blockC:$ret");
}

void main() {
  blockA(() {
    print("A");
  });
  
  blockB((arg1, arg2) {
    print("B: $arg1,$arg2");
  });
  
  blockC((arg1, arg2) {
    print("C: $arg1,$arg2");
    return arg1 + arg2;
  });
}

// A
// B: 1,2
// C: 1,2
// blockC:3
```

通过 `typedef` 封装参数：

```dart
typedef void CallBackA();
typedef void CallBackB(int arg1, int arg2);
typedef int CallBackC(int arg1, int arg2);

void blockE(CallBackA callBackA) {
  callBackA();
}

void blockF(CallBackB callBackB) {
  callBackB(1, 2);
}

void blockG(CallBackC callBackC) {
  int ret = callBackC(1, 2);
}

void main(List<String> args) {
  blockE(() {});
  blockF((arg1, arg2) {});
  blockG((arg1, arg2) => arg1 + arg2);
}
```
