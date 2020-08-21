
# 使用场景

## 两个时间对比

```dart
DateTime _lastPressedAt;
if(DateTime.now().difference(_lastPressedAt) > Duration(seconds: 2)){}
```