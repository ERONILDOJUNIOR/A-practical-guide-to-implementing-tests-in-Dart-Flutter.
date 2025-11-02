## **06 — Testes Assíncronos**

# 📘 Testes Assíncronos

[← Fluxo e Controle de Testes](../05_fluxo_controle/05_fluxo_controle_pt.md) | [Mocks e Stubs →](../07_mocking/07_mocking_pt.md)

Em Dart e Flutter, muitos recursos são **assíncronos**, como `Future`s, `Stream`s e chamadas de rede.
Os testes assíncronos permitem **verificar valores que serão produzidos no futuro**, garantindo que a lógica do código funcione corretamente.

### 🔑 Estrutura de Testes Assíncronos

* Use `async` no callback do teste.
* Use `await` para esperar que o `Future` complete.
* Use `expectLater` com **matchers assíncronos**.

```dart
import 'package:test/test.dart';

Future<int> fetchNumber() async {
  await Future.delayed(Duration(milliseconds: 100));
  return 42;
}

void main() {
  test('Future deve retornar 42', () async {
    final result = await fetchNumber();
    expect(result, equals(42));
  });
}
```

### 🌊 Testando Streams

Streams são sequências de eventos ao longo do tempo.
Use `expectLater` com `emits` ou `emitsInOrder` para verificar os valores emitidos:

```dart
Stream<int> countStream() async* {
  yield 1;
  yield 2;
  yield 3;
}

void main() {
  test('Stream deve emitir valores 1, 2, 3', () async {
    await expectLater(countStream(), emitsInOrder([1, 2, 3]));
  });
}
```

### 💡 Boas Práticas

* Sempre **await** os testes assíncronos para garantir que terminem antes da finalização do runner.
* Use **`setUp` e `tearDown`** para preparar e limpar recursos assíncronos.
* Prefira **matchers assíncronos** (`completion`, `emits`, `throwsA`) em vez de `expect()` simples.
* Evite usar `sleep` ou delays manuais nos testes.

---

[← Fluxo e Controle de Testes](../05_fluxo_controle/05_fluxo_controle_pt.md) | [Mocks e Stubs →](../07_mocking/07_mocking_pt.md)
