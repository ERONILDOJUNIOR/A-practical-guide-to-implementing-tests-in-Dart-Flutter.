## **07 — Mock e Stub**

[← Testes Assíncronos](../06_assincronos/06_assincronos_pt.md) | [Testes de Integração →](../08_integracao/08_integracao_pt.md)

# 📘 Mock e Stub

Mocks e Stubs são usados para **simular dependências externas** em testes, garantindo **isolamento** e **previsibilidade** do comportamento do código.

* **Stub:** Fornece respostas pré-definidas para chamadas de métodos, sem registrar interações.
* **Mock:** Além de fornecer respostas, permite **verificar chamadas e interações**.

### 🔑 Configuração com `mocktail`

1. Adicione o pacote no `pubspec.yaml`:

```bash
flutter pub add mocktail
```

2. Crie uma classe mock:

```dart
import 'package:mocktail/mocktail.dart';
import 'package:my_app/services/auth_service.dart';

class MockAuthService extends Mock implements AuthService {}
```

### 🏗️ Exemplo de Uso

```dart
void main() {
  late MockAuthService mockService;

  setUp(() {
    mockService = MockAuthService();
  });

  test('Deve retornar usuário autenticado', () async {
    when(() => mockService.login('user', 'pass'))
        .thenAnswer((_) async => true);

    final result = await mockService.login('user', 'pass');
    expect(result, isTrue);

    verify(() => mockService.login('user', 'pass')).called(1);
  });
}
```

### 💡 Dicas de Boas Práticas

* **Use mocks** para dependências externas como APIs, bancos de dados e serviços.
* **Verifique interações** usando `verify()` para garantir que métodos foram chamados corretamente.
* Prefira **stubs** quando não for necessário verificar chamadas, apenas resultados.
* **Resete mocks** entre testes usando `reset()` se necessário.

---

[← Testes Assíncronos](../06_assincronos/06_assincronos_pt.md) | [Testes de Integração →](../08_integracao/08_integracao_pt.md)
