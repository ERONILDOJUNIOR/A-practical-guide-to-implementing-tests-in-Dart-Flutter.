## **08 — Integration Testing**

[← Mocking and Stubs](../07_mocking/07_mocking_en.md) | [Coverage and CI/CD →](../09_cobertura/09_cobertura_en.md)

# 📘 Integration Testing

**Integration tests** verify whether **different parts of the system work correctly together**, integrating real components such as services, databases, and UI.

In Flutter, this type of test is essential to validate **the full user flow**, simulating real user interactions.

---

### 🧩 Integration Test Structure

In Flutter, integration tests usually live under:

```
integration_test/
```

Example structure:

```
lib/
  main.dart
integration_test/
  app_test.dart
test/
  unit/
  widget/
```

---

### 🚀 Example with `integration_test`

1. Add the dependency:

```bash
flutter pub add integration_test --dev
```

2. Create `integration_test/app_test.dart`:

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:integration_test/integration_test.dart';
import 'package:my_app/main.dart' as app;

void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();

  testWidgets('Full login flow', (tester) async {
    app.main();
    await tester.pumpAndSettle();

    final userField = find.byKey(const Key('user_field'));
    final passField = find.byKey(const Key('password_field'));
    final loginButton = find.byKey(const Key('login_button'));

    await tester.enterText(userField, 'user');
    await tester.enterText(passField, 'pass');
    await tester.tap(loginButton);
    await tester.pumpAndSettle();

    expect(find.text('Welcome!'), findsOneWidget);
  });
}
```

---

### 🔍 Running the Tests

To run integration tests:

```bash
flutter test integration_test
```

or

```bash
flutter drive --driver=test_driver/integration_test.dart --target=integration_test/app_test.dart
```

---

### 💡 Best Practices

* Use **unique `Key`s** to identify UI elements.
* Run integration tests in **controlled environments** with predictable dependencies.
* Automate tests with **CI/CD tools** (GitHub Actions, Bitrise, Codemagic).
* Combine **mocked services** with **real behaviors** only when needed.

---

[← Mocking and Stubs](../07_mocking/07_mocking_en.md) | [Coverage and CI/CD →](../09_cobertura/09_cobertura_en.md)
