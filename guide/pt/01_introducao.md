# 🧭 Introdução ao Ecossistema de Testes em Dart e Flutter

Os testes em Dart e Flutter são baseados em funções de alto nível providas pelos pacotes:

- `package:test`: testes de lógica e unidades puras (Dart).
- `package:flutter_test`: testes de widgets e integração (Flutter).

A execução de testes é controlada por meio da função principal `main()` e organizada com blocos de `group()` e `test()`.

```dart
import 'package:test/test.dart';

void main() {
  group('Operações Matemáticas', () {
    test('Soma deve retornar valor correto', () {
      final result = 2 + 2;
      expect(result, equals(4));
    });
  });
}
```

---

## 🔍 Tipos de Teste

| Tipo | Descrição | Biblioteca |
|------|------------|-------------|
| **Unitário** | Testa pequenas unidades isoladas de código. | `package:test` |
| **De Widget** | Testa a renderização e comportamento de Widgets. | `package:flutter_test` |
| **De Integração** | Verifica a interação entre múltiplos módulos e camadas. | `flutter_driver` (ou `integration_test`) |
