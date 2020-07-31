
# 平台支持

## [macOS](https://flutter.dev/desktop)

```sh
flutter channel master
flutter upgrade
flutter config --enable-macos-desktop # --enable-web --enable-linux-desktop --enable-windows-desktop --enable-android-embedding-v2
export ENABLE_FLUTTER_DESKTOP=true
flutter doctor
flutter devices
# run
flutter run -d macos
# build
flutter build macos
```

## [web](https://flutter.cn/docs/get-started/web)

```sh
flutter channel beta
flutter upgrade
flutter config --enable-web
```