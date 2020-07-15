
[TextCapitalization Class](https://api.flutter.dev/flutter/services/TextCapitalization-class.html)

```dart
enum TextCapitalization {
  words, // 每个单词的首个大写的键盘。iOS: UITextAutocapitalizationTypeWords ，Android: InputType.TYPE_TEXT_FLAG_CAP_WORDS
  sentences, // 每个句子的首个大写的键盘。iOS: UITextAutocapitalizationTypeSentences ，Android: InputType.TYPE_TEXT_FLAG_CAP_SENTENCES
  characters, // 每个字符大写的键盘。iOS: UITextAutocapitalizationTypeAllCharacters ，Android: InputType.TYPE_TEXT_FLAG_CAP_CHARACTERS
  none,// 默认小写键盘
}
```