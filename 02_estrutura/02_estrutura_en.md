## **02 — Test Structure in Dart & Flutter**

[← Introduction](../01_introducao/01_introducao_en.md) | [Assertions →](../03_assertions/03_assertions_en.md)

# 📘 Structure

The **test structure** in Dart and Flutter follows a hierarchical organization that enhances **readability, maintainability, and execution**.

The entry point is always the `main()` function, within which we can create **groups (`group`)** and **test cases (`test` or `testWidgets`)**.

### 🏗️ Basic Organization

```dart
import 'package:flutter_test/flutter_test.dart';

void main() {
  group('User Class Test Group', () {
    setUp(() {
      // Preparation before each test
    });

    tearDown(() {
      // Cleanup after each test
    });

    test('Should create a user correctly', () {
      // Test logic
    });

    test('Should throw exception for invalid data', () {
      // Test logic
    });
  });
}
```

### 📌 Main Functions

| Function                         | Description                        | When to Use                                  |
| -------------------------------- | ---------------------------------- | -------------------------------------------- |
| `main()`                         | Entry point of the test file       | Always required                              |
| `group(description, body)`       | Groups related tests               | Organize tests by module, class, or feature  |
| `test(description, body)`        | Defines a unit test                | Pure logic tests (functions, methods)        |
| `testWidgets(description, body)` | Defines a widget test              | Tests that interact with Flutter UI          |
| `setUp(callback)`                | Runs before each test in the group | Initialize objects or necessary variables    |
| `tearDown(callback)`             | Runs after each test in the group  | Clean up states or close streams             |
| `setUpAll(callback)`             | Runs once before the first test    | Global initialization or expensive resources |
| `tearDownAll(callback)`          | Runs once after the last test      | Global cleanup of resources                  |

### 🔄 Execution Flow

1. `setUpAll()` → executed **once** before all tests.
2. For each test:

   * `setUp()` → prepares the test environment.
   * `test()` or `testWidgets()` → runs the test.
   * `tearDown()` → cleans up after the test.
3. `tearDownAll()` → executed **once** after all tests in the group.

### 🧭 Recommended Folder Structure

```
test/
├── models/
│   └── user_model_test.dart
├── services/
│   └── auth_service_test.dart
├── widgets/
│   └── login_form_test.dart
└── integration/
    └── login_flow_test.dart
```

* Each file should represent **a logical unit** of testing.
* Name files with `_test.dart` so the Dart/Flutter runner recognizes them automatically.

---

[← Introduction](../01_introducao/01_introducao_en.md) | [Assertions →](../03_assertions/03_assertions_en.md)
