## **04 — Hooks and Lifecycle**

[← Assertions](../03_assertions/03_assertions_en.md) | [Test Flow and Control →](../05_fluxo_controle/05_fluxo_controle_en.md)

# 📘 Hooks

In the Dart/Flutter testing ecosystem, **hooks** are functions that allow you to **setup and teardown** the test environment before and after executing each test or group.
They ensure **isolation**, preventing tests from affecting each other.

### 🔑 Main Hooks

| Function                | Scope                    | Execution                  | Usage                                        |
| ----------------------- | ------------------------ | -------------------------- | -------------------------------------------- |
| `setUp(callback)`       | Inside `group` or `main` | Before **each** test       | Initialize objects, mocks, or variables      |
| `tearDown(callback)`    | Inside `group` or `main` | After **each** test        | Clean up states or close streams             |
| `setUpAll(callback)`    | Inside `group` or `main` | Once before the first test | Global initialization or expensive resources |
| `tearDownAll(callback)` | Inside `group` or `main` | Once after the last test   | Close global connections                     |

### 🏗️ Example Usage

```dart
import 'package:flutter_test/flutter_test.dart';

void main() {
  late UserService service;

  group('UserService Tests', () {
    setUpAll(() {
      // Initialize expensive resources once before all tests
    });

    setUp(() {
      service = UserService(); // fresh state for each test
    });

    tearDown(() {
      service.dispose(); // cleanup after each test
    });

    tearDownAll(() {
      // Global cleanup if necessary
    });

    test('Should create user correctly', () {
      final user = service.createUser('Alice');
      expect(user.name, equals('Alice'));
    });

    test('Should throw exception if name is empty', () {
      expect(() => service.createUser(''), throwsA(isA<ArgumentError>()));
    });
  });
}
```

### 💡 Best Practices

* **Use setUp/tearDown** to keep tests **independent**.
* **Avoid expensive initialization** in `setUp()`; prefer `setUpAll()` for global resources.
* Always **cleanup resources** (streams, connections, mocks) in `tearDown()`.

---

[← Assertions](../03_assertions/03_assertions_en.md) | [Test Flow and Control →](../05_fluxo_controle/05_fluxo_controle_en.md)
