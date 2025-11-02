# 🧭 Introduction to the Dart and Flutter Testing Ecosystem

Testing in Dart and Flutter relies on high-level functions provided by:

- `package:test`: for logic and unit tests (pure Dart).
- `package:flutter_test`: for widget and integration tests (Flutter).

The test execution starts from the main function `main()` and is organized using `group()` and `test()` blocks.

```dart
import 'package:test/test.dart';

void main() {
  group('Math Operations', () {
    test('Sum should return the correct value', () {
      final result = 2 + 2;
      expect(result, equals(4));
    });
  });
}
```

---

## 🔍 Test Types

| Type | Description | Library |
|------|--------------|----------|
| **Unit Test** | Tests small, isolated units of code. | `package:test` |
| **Widget Test** | Tests widget rendering and behavior. | `package:flutter_test` |
| **Integration Test** | Checks interactions between multiple modules and layers. | `flutter_driver` (or `integration_test`) |
