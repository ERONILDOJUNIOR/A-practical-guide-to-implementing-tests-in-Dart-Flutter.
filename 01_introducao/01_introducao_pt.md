## 🇧🇷 **Introdução — Guia de Testes em Dart e Flutter**

[Estrutura de Testes →](../02_estrutura/02_estrutura_pt.md)

# 📘 Introdução

O ecossistema de testes em **Dart e Flutter** é uma das partes mais robustas e bem documentadas do framework, oferecendo suporte para testes **unitários**, **de widget** e **de integração**.
Com ele, é possível validar desde a **lógica de negócio** até o **comportamento visual** de componentes da interface.

### 🎯 Objetivo do Guia

Este guia tem como objetivo apresentar uma **visão prática e sistematizada** sobre como estruturar, escrever e automatizar testes em Dart e Flutter, servindo como referência para desenvolvedores e pesquisadores que buscam **melhoria de qualidade de software** e **análise de padrões de teste**.

### 🧩 Tipos de Teste

O ambiente de testes do Flutter é dividido em três níveis principais:

| Tipo de Teste        | Escopo                                    | Exemplo de Aplicação                                   |
| -------------------- | ----------------------------------------- | ------------------------------------------------------ |
| **Unit Test**        | Testa funções e classes isoladamente.     | Validar cálculos, parse de dados ou lógica de negócio. |
| **Widget Test**      | Testa componentes visuais em isolamento.  | Verificar comportamento e renderização de Widgets.     |
| **Integration Test** | Testa o app completo em um ambiente real. | Simular fluxo de usuário e integração entre módulos.   |

### ⚙️ Estrutura Básica

Um arquivo de teste em Dart deve conter a função `main()` como ponto de entrada, seguida de **grupos de testes (`group`)** e **casos de teste (`test`)**.
Exemplo básico:

```dart
import 'package:flutter_test/flutter_test.dart';

void main() {
  group('Cálculo de Soma', () {
    test('Deve somar dois valores corretamente', () {
      final resultado = 2 + 3;
      expect(resultado, equals(5));
    });
  });
}
```

### 🧭 Organização Recomendada

* Crie uma pasta `test/` na raiz do projeto.
* Nomeie cada arquivo com o sufixo `_test.dart`.
* Estruture por módulo ou funcionalidade, por exemplo:

  ```
  test/
  ├── models/
  │   └── user_model_test.dart
  ├── services/
  │   └── auth_service_test.dart
  └── widgets/
      └── login_form_test.dart
  ```

### 💡 Boas Práticas

* Cada teste deve ser **independente** dos demais.
* Use **mocks** para dependências externas.
* Prefira **nomes descritivos** para os testes.
* Utilize **setUp()** e **tearDown()** para preparar e limpar o ambiente.

### 📦 Pacotes Importantes

Os principais pacotes utilizados são:

* `test`: para testes unitários em Dart puro.
* `flutter_test`: para testes de widgets e integração.
* `mocktail`: para simulação de dependências (mocks e stubs).

---

[Estrutura de Testes →](../02_estrutura/02_estrutura_pt.md)
