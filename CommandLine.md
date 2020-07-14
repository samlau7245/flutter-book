
* 打印可用设备

# 全局命令

```sh
-h, --help                  帮助文档
-v, --verbose               详细日志
-d, --device-id             可用设备列表、ID
    --version               版本号
    --suppress-analytics    禁止分析日志
    --packages              
```

# 可使用的命令

```sh
analyze           # Analyze the project's Dart code.
assemble          # Assemble and build flutter resources.
attach            # Attach to a running application.
bash-completion   # Output command line shell completion setup scripts.
build             # Flutter build commands.
channel           # List or switch flutter channels.
clean             # Delete the build/ and .dart_tool/ directories.
config            # Configure Flutter settings.
create            # Create a new Flutter project.
devices           # List all connected devices.
doctor            # Show information about the installed tooling.
downgrade         # Downgrade Flutter to the last active version for the current channel.
drive             # Runs Flutter Driver tests for the current project.
emulators         # List, launch and create emulators.
format            # Format one or more dart files.
install           # Install a Flutter app on an attached device.
logs              # Show log output for running Flutter apps.
precache          # Populates the Flutter tool's cache of binary artifacts.
pub               # Commands for managing Flutter packages.
run               # Run your Flutter app on an attached device.
screenshot        # Take a screenshot from a connected device.
symbolize         # Symbolize a stack trace from an AOT compiled flutter application.
test              # Run Flutter unit tests for the current project.
upgrade           # 更新 Flutter
version           # 查看 Flutter 版本
```

## creat

```sh
    --platforms # 平台：[ios (default), android (default), windows (default), linux (default), macos (default), web (default)]
    --[no-]pub # 当项目创建好了以后是否执行 "flutter pub get" (defaults to on)
    --[no-]offline # 
    --[no-]with-driver-test # 
-t, --template=<type> # type：[app]、[module]、[package]、[plugin]
-s, --sample=<id>             
    --list-samples=<path>
    --[no-]overwrite # 重写已存在的文件
    --description # 项目描述，写在 pubspec.yaml 中 `description` 字段。 (defaults to "A new Flutter project.")
    --org # 以反向域名表示法来指定你的组织。该值用于生成的 Android 及 iOS 代码。 This string is used in Java package names and as prefix in the iOS bundle identifier.
    --project-name # 项目名
-i, --ios-language # 指定 iOS 的语言 [objc, swift (default)]
-a, --android-language # 指定 Android 的语言 [java, kotlin (default)]
```


































