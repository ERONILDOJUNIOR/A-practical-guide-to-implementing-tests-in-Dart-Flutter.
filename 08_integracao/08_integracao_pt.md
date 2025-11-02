## **08 — Testes de Integração**

[← Mocks e Stubs](../07_mocking/07_mocking_pt.md) | [Cobertura e CI/CD →](../09_cobertura/09_cobertura_pt.md)

# 📘 Testes de Integração

Os **testes de integração** verificam se **diferentes partes do sistema funcionam corretamente em conjunto**, integrando componentes reais como serviços, banco de dados, e interface de usuário.

Em Flutter, esse tipo de teste é essencial para validar **o fluxo completo da aplicação**, simulando interações reais de usuário.

---

### 🧩 Estrutura de Teste de Integração

No Flutter, os testes de integração geralmente vivem no diretório:

```
integration_test/
```

Exemplo de estrutura:

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

### 🚀 Exemplo com `integration_test`

1. Adicione a dependência:

```bash
flutter pub add integration_test --dev
```

2. Crie o arquivo `integration_test/app_test.dart`:

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:integration_test/integration_test.dart';
import 'package:my_app/main.dart' as app;

void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();

  testWidgets('Fluxo completo de login', (tester) async {
    app.main();
    await tester.pumpAndSettle();

    final userField = find.byKey(const Key('user_field'));
    final passField = find.byKey(const Key('password_field'));
    final loginButton = find.byKey(const Key('login_button'));

    await tester.enterText(userField, 'user');
    await tester.enterText(passField, 'pass');
    await tester.tap(loginButton);
    await tester.pumpAndSettle();

    expect(find.text('Bem-vindo!'), findsOneWidget);
  });
}
```

---

### 🔍 Execução

Para rodar um teste de integração:

```bash
flutter test integration_test
```

ou

```bash
flutter drive --driver=test_driver/integration_test.dart --target=integration_test/app_test.dart
```

---

### 💡 Boas Práticas

* Use **chaves (`Key`) únicas** para identificar elementos na UI.
* Execute testes de integração em **ambientes controlados**, com dependências previsíveis.
* Automatize os testes com **CI/CD (GitHub Actions, Bitrise, Codemagic)**.
* Combine **mocking** de serviços com **comportamentos reais** apenas quando necessário.

---

[← Mocks e Stubs](../07_mocking/07_mocking_pt.md) | [Cobertura e CI/CD →](../09_cobertura/09_cobertura_pt.md)
