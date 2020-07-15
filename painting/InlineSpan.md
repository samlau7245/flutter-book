
[TextSpan Class](https://api.flutter.dev/flutter/painting/TextSpan-class.html)

# 构造函数

## InlineSpan

```dart
const InlineSpan({
	TextStyle style
})
```

## TextSpan

```dart
const TextSpan({
	String text,
	List<InlineSpan> children,
	TextStyle style,
	GestureRecognizer recognizer,
	String semanticsLabel
})
```

## PlaceholderSpan

```dart
const PlaceholderSpan({
	PlaceholderAlignment alignment: ui.PlaceholderAlignment.bottom,
	TextBaseline baseline,
	TextStyle style
})
```

### WidgetSpan

```dart
const WidgetSpan({
	@required Widget child,
	PlaceholderAlignment alignment: ui.PlaceholderAlignment.bottom,
	TextBaseline baseline,
	TextStyle style
})
```