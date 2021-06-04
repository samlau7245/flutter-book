> 通过 `LayoutBuilder` 来创建一个自适应UI

首先创建一个简单的联系人界面：


```dart
import 'dart:convert';

import 'package:adaptive/models/data.dart';
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: '通讯录',
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({Key? key}) : super(key: key);

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  late List<Data> contects;

  Future<String> loadContects() async {
    return await rootBundle.loadString('assets/contects.json');
  }

  @override
  void initState() {
    contects = <Data>[];

    loadContects().then((value) {
      var tmpt = <Data>[];
      for (var item in json.decode(value) as List) {
        Data data = Data.fromJson(item);
        tmpt.add(data);
      }

      setState(() {
        contects = tmpt;
      });
    });

    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('通讯录')),
      body: Container(
        child: ListView.builder(
          itemBuilder: (_, index) {
            return ListTile(
              title: Text(this.contects[index].name),
              onTap: () {
                Navigator.of(context)
                    .push(ContectDetail.route(this.contects[index]));
              },
            );
          },
          itemCount: this.contects.length,
        ),
      ),
    );
  }
}

class ContectDetail extends StatelessWidget {
  final Data data;
  const ContectDetail({Key? key, required this.data}) : super(key: key);

  static Route route(Data data) =>
      MaterialPageRoute(builder: (_) => ContectDetail(data: data));

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(this.data.address),
            Text(this.data.tel),
            ElevatedButton(onPressed: () {}, child: Text('Contect Me')),
          ],
        ),
      ),
    );
  }
}
```

远程仓库：

```dart
git clone -b ui_adaptive https://gitee.com/flutter-slu/examples.git
cd /examples
git checkout 3031e08ce04073243fea1350cdd90c3bc3b0d058
```

> 下一阶段的操作： 当屏幕宽度 > 600px 的时候，不用 PUSH，Detail 和 List 同时存在一个界面内。



```dart
import 'dart:convert';

import 'package:adaptive/models/data.dart';
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: '通讯录',
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({Key? key}) : super(key: key);

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  late List<Data> contects;
  Data? selectedData;

  Future<String> loadContects() async {
    return await rootBundle.loadString('assets/contects.json');
  }

  @override
  void initState() {
    contects = <Data>[];

    loadContects().then((value) {
      var tmpt = <Data>[];
      for (var item in json.decode(value) as List) {
        Data data = Data.fromJson(item);
        tmpt.add(data);
      }

      setState(() {
        contects = tmpt;
      });
    });

    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('通讯录')),
      body: LayoutBuilder(
        builder: (context, constraints) {
          if (constraints.maxWidth > 600) {
            return Row(
              children: [
                Expanded(
                  child: ContectListLayout(
                    contects: contects,
                    onTapCallBack: (value) {
                      setState(() {
                        selectedData = value;
                      });
                    },
                  ),
                  flex: 1,
                ),
                Expanded(
                  child: selectedData == null
                      ? Placeholder()
                      : ContectDetail(data: selectedData!),
                  flex: 4,
                ),
              ],
            );
          }

          return ContectListLayout(
            contects: contects,
            onTapCallBack: (data) {
              Navigator.of(context).push(ContectDetail.route(data));
            },
          );
        },
      ),
    );
  }
}

class ContectListLayout extends StatelessWidget {
  const ContectListLayout({
    Key? key,
    required this.contects,
    required this.onTapCallBack,
  }) : super(key: key);

  final List<Data> contects;
  final ValueChanged<Data> onTapCallBack;

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemBuilder: (_, index) {
        return ListTile(
          title: Text(this.contects[index].name),
          onTap: () => this.onTapCallBack(this.contects[index]),
        );
      },
      itemCount: this.contects.length,
    );
  }
}

class ContectDetail extends StatelessWidget {
  final Data data;
  const ContectDetail({Key? key, required this.data}) : super(key: key);

  static Route route(Data data) => MaterialPageRoute(
        builder: (_) => Scaffold(
          appBar: AppBar(),
          body: ContectDetail(data: data),
        ),
      );

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          Text(this.data.address),
          Text(this.data.tel),
          ElevatedButton(onPressed: () {}, child: Text('Contect Me')),
        ],
      ),
    );
  }
}
```

<img src="/assets/images/ui/01.png"/>

完整代码：

```bash
git clone -b ui_adaptive https://gitee.com/flutter-slu/examples.git
cd /examples
git checkout 84735e3af63d9e32f24fd7ec3a4f1d16ddc7d86f
```