> 使用Bloc框架实现一个简单的天气APP，真实请求接口，实现刷新功能。

初始化项目：

```bash
git clone -b bloc_login https://gitee.com/flutter-slu/examples.git
cd examples/
git checkout 2eac32855d280cc15d039d7a40416ea942be51b8
```

# 效果

<img src="/assets/images/tutorial/state/09.gif"/>

# 结构

```
.
├── assets
│   ├── clear.png
│   ├── cloudy.png
│   ├── rainy.png
│   ├── snow.png
│   └── thunderstorm.png
├── lib
│   ├── app.dart
│   ├── main.dart
│   ├── search
│   │   ├── search.dart
│   │   └── view
│   │       └── search_page.dart
│   ├── settings
│   │   ├── settings.dart
│   │   └── view
│   │       └── settings_page.dart
│   ├── theme
│   │   ├── cubit
│   │   │   └── theme_cubit.dart
│   │   └── theme.dart
│   ├── weather
│   │   ├── cubit
│   │   │   ├── weather_cubit.dart
│   │   │   ├── weather_cubit.g.dart
│   │   │   └── weather_state.dart
│   │   ├── models
│   │   │   ├── models.dart
│   │   │   ├── weather.dart
│   │   │   └── weather.g.dart
│   │   ├── view
│   │   │   └── weather_page.dart
│   │   ├── weather.dart
│   │   └── widgets
│   │       ├── weather_empty.dart
│   │       ├── weather_error.dart
│   │       ├── weather_loading.dart
│   │       ├── weather_populated.dart
│   │       └── widgets.dart
│   └── weather_bloc_observer.dart
├── packages
│   ├── meta_weather_api
│   │   ├── lib
│   │   │   ├── meta_weather_api.dart
│   │   │   └── src
│   │   │       ├── meta_weather_api_client.dart
│   │   │       └── models
│   │   │           ├── location.dart
│   │   │           ├── location.g.dart
│   │   │           ├── models.dart
│   │   │           ├── weather.dart
│   │   │           └── weather.g.dart
│   │   └── pubspec.yaml
│   └── weather_repository
│       ├── lib
│       │   ├── src
│       │   │   ├── models
│       │   │   │   ├── models.dart
│       │   │   │   ├── weather.dart
│       │   │   │   └── weather.g.dart
│       │   │   └── weather_repository.dart
│       │   └── weather_repository.dart
│       └── pubspec.yaml
└── pubspec.yaml
```

# pubspec.yaml

```dart
name: bloc_weather
description: A new Flutter project.
publish_to: 'none' # Remove this line if you wish to publish to pub.dev
version: 1.0.0+1

environment:
  sdk: ">=2.12.0 <3.0.0"

dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
  flutter_bloc: ^7.0.1
  http: ^0.13.3
  equatable: ^2.0.2

dev_dependencies:
  flutter_test:
    sdk: flutter
flutter:
  uses-material-design: true
  assets:
    - assets/
```

# 数据准备

使用API的官网:[metaweather API](https://www.metaweather.com/zh/)。

* `/api/location/search/?query=$city` 输入城市名查询位置。

```json
[
  {
    "title": "London",
    "location_type": "City",
    "woeid": 44418,
    "latt_long": "51.506321,-0.12714"
  }
]
```

* `/api/location/$locationId` 通过位置查询天气。


# packages

## meta_weather_api 天气API封装

### meta_weather_api_client.dart

`MetaWeatherApiClient` 类负责管理天气的API。

## weather_repository 天气数据包

















































