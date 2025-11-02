## **03 — Assertions em Dart e Flutter**

[← Estrutura de Testes](../02_estrutura/02_estrutura_pt.md) | [Hooks e Ciclo de Vida →](../04_hooks/04_hooks_pt.md)

# 📘 Assertions

As **assertions** são o coração de qualquer teste, permitindo verificar se o resultado real (`actual`) corresponde ao resultado esperado (`expected`).
No Dart/Flutter, usamos principalmente `expect()` para testes síncronos e `expectLater()` para testes assíncronos.

### 🛠️ Funções Principais

| Função                                         | Descrição                                               | Quando Usar                     |
| ---------------------------------------------- | ------------------------------------------------------- | ------------------------------- |
| `expect(actual, matcher, {reason, skip})`      | Verifica o valor imediatamente                          | Para testes **síncronos**       |
| `expectLater(actual, matcher, {reason, skip})` | Retorna um `Future` que verifica o valor posteriormente | Para **Streams** ou **Futures** |

**Exemplo Síncrono:**

```dart
import 'package:test/test.dart';

void main() {
  test('Deve somar corretamente', () {
    final resultado = 2 + 3;
    expect(resultado, equals(5));
  });
}
```

**Exemplo Assíncrono:**

```dart
import 'package:test/test.dart';

void main() {
  test('Deve completar o Future', () async {
    final futuro = Future.value(42);
    await expectLater(futuro, completion(equals(42)));
  });
}
```

### 🔍 Matchers Comuns

| Categoria             | Matcher                                     | Descrição                                |
| --------------------- | ------------------------------------------- | ---------------------------------------- |
| Igualdade             | `equals(valor)`                             | Verifica igualdade exata                 |
| Tipo                  | `isA<T>()`                                  | Verifica tipo do objeto                  |
| Booleano              | `isTrue` / `isFalse`                        | Verifica valor booleano                  |
| Nulo                  | `isNull` / `isNotNull`                      | Verifica nulidade                        |
| Coleções              | `isEmpty` / `isNotEmpty` / `contains(item)` | Verifica listas, mapas e sets            |
| Exceções (síncrono)   | `throwsA(isA<TipoExcecao>())`               | Verifica exceções lançadas               |
| Exceções (assíncrono) | `throwsA(...)`                              | Verifica exceções em Futures             |
| Future                | `completes` / `completion(matcher)`         | Verifica se Future completa corretamente |
| Streams               | `emits(matcher)`                            | Verifica valores emitidos por Streams    |

### 💡 Dicas de Uso

* Use `expect()` para **valores imediatos**.
* Use `await expectLater()` para **valores futuros ou Streams**.
* Sempre forneça o parâmetro `reason` para mensagens mais claras em falhas.

---

[← Estrutura de Testes](../02_estrutura/02_estrutura_pt.md) | [Hooks e Ciclo de Vida →](../04_hooks/04_hooks_pt.md)
