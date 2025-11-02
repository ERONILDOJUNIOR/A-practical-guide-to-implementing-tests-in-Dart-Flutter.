## **06 — Async Testing**

[← Test Flow and Control](../05_fluxo_controle/05_fluxo_controle_en.md) | [Mocking and Stubs →](../07_mocking/07_mocking_en.md)

# 📘 Async Testing

In Dart and Flutter, many features are **asynchronous**, such as `Future`s, `Stream`s, and network calls.
Async tests allow you to **verify values produced in the future**, ensuring the logic behaves correctly.

### 🔑 Async Test Structure

* Use `async` in the test callback.
* Use `await` to wait for the `Future` to complete.
* Use `expectLater` with **asynchronous matchers**.

```dart
import 'package:test/test.dart';

Future<int> fetchNumber() async {
  await Future.delayed(Duration(milliseconds: 100));
  return 42;
}

void main() {
  test('Future should return 42', () async {
    final result = await fetchNumber();
    expect(result, equals(42));
  });
}
```

### 🌊 Testing Streams

Streams are sequences of events over time.
Use `expectLater` with `emits` or `emitsInOrder` to verify emitted values:

```dart
Stream<int> countStream() async* {
  yield 1;
  yield 2;
  yield 3;
}

void main() {
  test('Stream should emit values 1, 2, 3', () async {
    await expectLater(countStream(), emitsInOrder([1, 2, 3]));
  });
}
```

### 💡 Best Practices

* Always **await** async tests to ensure they complete before the runner finishes.
* Use **`setUp` and `tearDown`** to prepare and clean asynchronous resources.
* Prefer **async matchers** (`completion`, `emits`, `throwsA`) over simple `expect()`.
* Avoid using `sleep` or manual delays in tests.

---

[← Test Flow and Control](../05_fluxo_controle/05_fluxo_controle_en.md) | [Mocking and Stubs →](../07_mocking/07_mocking_en.md)
