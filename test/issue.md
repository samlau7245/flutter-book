
```sh
Command PhaseScriptExecution failed with a nonzero exit code
note: Using new build system
note: Building targets in parallel
note: Planning build
note: Constructing build description
warning: The iOS deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 4.3, but the range of supported deployment target versions is 8.0 to 13.5.99. (in target 'FMDB' from project 'Pods')
```

> 这是因为Xcode版本太高的原因，修改Xcode编译系统：在Xcode菜单栏选择File -> Workspace Setting -> Build System 选择Legacy Build System 重新运行即可。

--- 

如果遇到项目运行过程中报错:

```sh
Undefined symbols for architecture arm64:
"_OBJC_CLASS_$_xxx", referenced from:
ld: symbol(s) not found for architecture arm64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

> 可以尝试把`ios`、`android` 文件夹删除，然后重新创建 `flutter create .`