
# 启动 DevTools

```sh
# 安装/更新 DevTools
% flutter pub global activate devtools

# 运行 DevTools
% flutter pub global run devtools
# Serving DevTools at http://127.0.0.1:9100
```

<img src="/assets/images/test/01.png"/>

# 启动项目的DeBug

```sh
% cd path/to/flutter/app
% flutter run
# An Observatory debugger and profiler on iPhone SE (2nd generation) is available at: http://127.0.0.1:56538/Ern0_yCMKoI=/
```

把`http://127.0.0.1:56538/Ern0_yCMKoI=/` URL 输入到`http://127.0.0.1:9100`地址的输入框中进行关联，启动DeBug。

<img src="/assets/images/test/02.png"/>

# 资料

* [我们用 Flutter 写了一套全新的 Flutter 开发者工具](https://mp.weixin.qq.com/s/4mcFo3z8DhCDkEMX7IPmww)
* [在 VS Code 里安装和使用开发者工具](https://flutter.cn/docs/development/tools/devtools/vscode)