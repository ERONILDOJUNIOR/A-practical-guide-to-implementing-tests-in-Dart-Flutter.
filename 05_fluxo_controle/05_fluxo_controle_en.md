## **05 — Test Flow and Control**

[← Hooks and Lifecycle](../04_hooks/04_hooks_en.md) | [Asynchronous Testing →](../06_assincronos/06_assincronos_en.md)

# 📘 Test Flow and Control

**Test flow and control** in Dart and Flutter allows you to **manage execution, skip tests, and organize output** in a structured way.

### ⏩ Skipping Tests

You can skip individual tests or entire groups using the `skip` parameter:

```dart
test('Temporarily disabled test', () {}, skip: true);

test('Test with reason to skip', () {}, skip: 'Feature still in development');

group('Skipped test group', () {
  test('This test will not run', () {});
}, skip: true);
```

> 💡 Skipping a `group` also skips all `test`s and hooks (`setUp`/`tearDown`) inside it.

### 📝 Description Messages

The **description** passed to `test()` or `group()` appears in the console and can be used to filter tests:

```dart
void main() {
  group('Authentication', () {
    test('Should allow login with valid credentials', () {
      // console: "Authentication Should allow login with valid credentials"
    });
  });
}
```

### 🔍 Running Specific Tests

You can run only certain tests from the terminal:

```bash
flutter test -n "login with valid credentials"
```

The `-n` flag accepts **regex**, allowing you to run tests with specific names.

### 🧭 Best Practices

* Give tests **descriptive and consistent names**.
* Use `skip` only for temporarily disabled features.
* Combine `group` with detailed descriptions for **readable reports**.

---

[← Hooks and Lifecycle](../04_hooks/04_hooks_en.md) | [Asynchronous Testing →](../06_assincronos/06_assincronos_en.md)
