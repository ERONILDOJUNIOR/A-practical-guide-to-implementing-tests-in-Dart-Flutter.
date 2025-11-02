## **02 — Estrutura de Testes em Dart e Flutter**

[← Introdução](../01_introducao/01_introducao_pt.md) | [Assertions →](../03_assertions/03_assertions_pt.md)

# 📘 Estrutura

A **estrutura de testes** em Dart e Flutter segue uma organização hierárquica que facilita **leitura, manutenção e execução**.

O ponto de partida é sempre a função `main()`, dentro da qual podemos criar **grupos (`group`)** e **casos de teste (`test` ou `testWidgets`)**.

### 🏗️ Organização Básica

```dart
import 'package:flutter_test/flutter_test.dart';

void main() {
  group('Grupo de Testes da Classe User', () {
    setUp(() {
      // Preparação antes de cada teste
    });

    tearDown(() {
      // Limpeza após cada teste
    });

    test('Deve criar um usuário corretamente', () {
      // Lógica de teste
    });

    test('Deve lançar exceção para dados inválidos', () {
      // Lógica de teste
    });
  });
}
```

### 📌 Funções Principais

| Função                           | Descrição                               | Quando Usar                                           |
| -------------------------------- | --------------------------------------- | ----------------------------------------------------- |
| `main()`                         | Entrada do arquivo de teste             | Sempre necessário                                     |
| `group(description, body)`       | Agrupa testes relacionados              | Organizar testes por módulo, classe ou funcionalidade |
| `test(description, body)`        | Define um teste unitário                | Testes de lógica pura (funções, métodos)              |
| `testWidgets(description, body)` | Define teste de widget                  | Testes que interagem com a interface do Flutter       |
| `setUp(callback)`                | Executa antes de cada teste no grupo    | Inicializar objetos ou variáveis necessárias          |
| `tearDown(callback)`             | Executa depois de cada teste no grupo   | Limpar estados ou fechar streams                      |
| `setUpAll(callback)`             | Executa uma vez antes do primeiro teste | Inicialização global ou de recursos caros             |
| `tearDownAll(callback)`          | Executa uma vez após o último teste     | Encerramento global de recursos                       |

### 🔄 Fluxo de Execução

1. `setUpAll()` → executado **uma vez** antes de todos os testes.
2. Para cada teste:

   * `setUp()` → prepara o ambiente do teste.
   * `test()` ou `testWidgets()` → executa o teste.
   * `tearDown()` → limpa o ambiente após o teste.
3. `tearDownAll()` → executado **uma vez** após todos os testes do grupo.

### 🧭 Organização Recomendada de Pastas

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

* Cada arquivo deve representar **uma unidade lógica** de teste.
* Nomeie com `_test.dart` para que o runner do Dart/Flutter reconheça automaticamente.

---

[← Introdução](../01_introducao/01_introducao_pt.md) | [Assertions →](../03_assertions/03_assertions_pt.md)
