## **04 — Hooks e Ciclo de Vida**

[← Assertions](../03_assertions/03_assertions_pt.md) | [Fluxo e Controle de Testes →](../05_fluxo_controle/05_fluxo_controle_pt.md)

# 📘 Hooks

No ecossistema de testes Dart/Flutter, **hooks** são funções que permitem **configurar e limpar o ambiente de teste** antes e depois da execução de cada teste ou grupo de testes.
Eles garantem **isolamento**, evitando que testes interfiram uns nos outros.

### 🔑 Hooks Principais

| Função                  | Escopo                      | Execução                        | Uso                                     |
| ----------------------- | --------------------------- | ------------------------------- | --------------------------------------- |
| `setUp(callback)`       | Dentro de `group` ou `main` | Antes de **cada** teste         | Inicializar objetos, mocks ou variáveis |
| `tearDown(callback)`    | Dentro de `group` ou `main` | Depois de **cada** teste        | Limpar estados ou fechar streams        |
| `setUpAll(callback)`    | Dentro de `group` ou `main` | Uma vez antes do primeiro teste | Inicialização global ou recursos caros  |
| `tearDownAll(callback)` | Dentro de `group` ou `main` | Uma vez após o último teste     | Fechar conexões globais                 |

### 🏗️ Exemplo de Uso

```dart
import 'package:flutter_test/flutter_test.dart';

void main() {
  late UserService service;

  group('Testes da UserService', () {
    setUpAll(() {
      // Inicializa algo pesado uma vez antes de todos os testes
    });

    setUp(() {
      service = UserService(); // novo estado para cada teste
    });

    tearDown(() {
      service.dispose(); // limpar recursos após cada teste
    });

    tearDownAll(() {
      // Cleanup global se necessário
    });

    test('Deve criar usuário corretamente', () {
      final user = service.createUser('Alice');
      expect(user.name, equals('Alice'));
    });

    test('Deve lançar exceção se nome vazio', () {
      expect(() => service.createUser(''), throwsA(isA<ArgumentError>()));
    });
  });
}
```

### 💡 Boas Práticas

* **Use setUp/tearDown** para manter testes **independentes**.
* **Evite inicializações pesadas** em `setUp()`; prefira `setUpAll()` se for global.
* Sempre **limpe recursos** (streams, conexões, mocks) no `tearDown()`.

---

[← Assertions](../03_assertions/03_assertions_pt.md) | [Fluxo e Controle de Testes →](../05_fluxo_controle/05_fluxo_controle_pt.md)
