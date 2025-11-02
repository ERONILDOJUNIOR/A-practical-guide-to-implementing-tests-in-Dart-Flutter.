## **03 — Assertions in Dart & Flutter**

[← Test Structure](../02_estrutura/02_estrutura_en.md) | [Hooks and Lifecycle →](../04_hooks/04_hooks_en.md)

# 📘 Assertions

**Assertions** are the core of any test, allowing you to verify if the actual result (`actual`) matches the expected result (`expected`).
In Dart/Flutter, we primarily use `expect()` for synchronous tests and `expectLater()` for asynchronous tests.

### 🛠️ Main Functions

| Function                                       | Description                                    | When to Use                    |
| ---------------------------------------------- | ---------------------------------------------- | ------------------------------ |
| `expect(actual, matcher, {reason, skip})`      | Checks the value immediately                   | For **synchronous** tests      |
| `expectLater(actual, matcher, {reason, skip})` | Returns a `Future` that checks the value later | For **Streams** or **Futures** |

**Synchronous Example:**

```dart
import 'package:test/test.dart';

void main() {
  test('Should add correctly', () {
    final result = 2 + 3;
    expect(result, equals(5));
  });
}
```

**Asynchronous Example:**

```dart
import 'package:test/test.dart';

void main() {
  test('Future should complete', () async {
    final future = Future.value(42);
    await expectLater(future, completion(equals(42)));
  });
}
```

### 🔍 Common Matchers

| Category           | Matcher                                     | Description                         |
| ------------------ | ------------------------------------------- | ----------------------------------- |
| Equality           | `equals(value)`                             | Checks exact equality               |
| Type               | `isA<T>()`                                  | Checks object type                  |
| Boolean            | `isTrue` / `isFalse`                        | Checks boolean value                |
| Null               | `isNull` / `isNotNull`                      | Checks nullability                  |
| Collections        | `isEmpty` / `isNotEmpty` / `contains(item)` | Checks lists, maps, sets            |
| Exceptions (sync)  | `throwsA(isA<ExceptionType>())`             | Checks thrown exceptions            |
| Exceptions (async) | `throwsA(...)`                              | Checks exceptions in Futures        |
| Future             | `completes` / `completion(matcher)`         | Verifies Future completes correctly |
| Streams            | `emits(matcher)`                            | Verifies emitted stream values      |

### 💡 Usage Tips

* Use `expect()` for **immediate values**.
* Use `await expectLater()` for **future values or streams**.
* Always provide the `reason` parameter for clearer failure messages.

---

[← Test Structure](../02_estrutura/02_estrutura_en.md) | [Hooks and Lifecycle →](../04_hooks/04_hooks_en.md)
