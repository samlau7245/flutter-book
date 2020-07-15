
[DropdownButtonFormField Class](https://api.flutter.dev/flutter/material/DropdownButtonFormField-class.html)

# 构造函数

```dart
DropdownButtonFormField<T>({
	Key key,
	T value,
	@required List<DropdownMenuItem<T>> items,
	DropdownButtonBuilder selectedItemBuilder,
	Widget hint,
	@required ValueChanged<T> onChanged,
	VoidCallback onTap,
	InputDecoration decoration: const InputDecoration(),
	FormFieldSetter<T> onSaved,
	FormFieldValidator<T> validator,
	bool autovalidate: false,
	Widget disabledHint,
	int elevation: 8,
	TextStyle style,
	Widget icon,
	Color iconDisabledColor,
	Color iconEnabledColor,
	double iconSize: 24.0,
	bool isDense: true,
	bool isExpanded: false,
	double itemHeight
})
```