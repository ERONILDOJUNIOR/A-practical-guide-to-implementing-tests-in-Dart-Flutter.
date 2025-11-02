## **07 — Mocking and Stubs**

[← Asynchronous Testing](../06_assincronos/06_assincronos_en.md) | [Integration Testing →](../08_integracao/08_integracao_en.md)

# 📘 Mocking and Stubs

Mocks and Stubs are used to **simulate external dependencies** in tests, ensuring **isolation** and **predictable behavior**.

* **Stub:** Provides predefined responses for method calls, without tracking interactions.
* **Mock:** Provides responses and also allows **verifying calls and interactions**.

### 🔑 Setup with `mocktail`

1. Add the package to `pubspec.yaml`:

```bash
flutter pub add mocktail
```

2. Create a mock class:

```dart
import 'package:mocktail/mocktail.dart';
import 'package:my_app/services/auth_service.dart';

class MockAuthService extends Mock implements AuthService {}
```

### 🏗️ Usage Example

```dart
void main() {
  late MockAuthService mockService;

  setUp(() {
    mockService = MockAuthService();
  });

  test('Should return authenticated user', () async {
    when(() => mockService.login('user', 'pass'))
        .thenAnswer((_) async => true);

    final result = await mockService.login('user', 'pass');
    expect(result, isTrue);

    verify(() => mockService.login('user', 'pass')).called(1);
  });
}
```

### 💡 Best Practices

* **Use mocks** for external dependencies like APIs, databases, and services.
* **Verify interactions** using `verify()` to ensure methods were called correctly.
* Prefer **stubs** when you only need to provide results without verifying calls.
* **Reset mocks** between tests using `reset()` if needed.

---

[← Asynchronous Testing](../06_assincronos/06_assincronos_en.md) | [Integration Testing →](../08_integracao/08_integracao_en.md)
