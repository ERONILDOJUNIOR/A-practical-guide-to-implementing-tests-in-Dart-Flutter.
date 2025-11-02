## **09 — Cobertura e Automação (CI/CD)**

[← Testes de Integração](../08_integracao/08_integracao_pt.md) | [Referências e Recursos →](../10_referencias/10_referencias_pt.md)

# 📘 Cobertura de Testes e Integração Contínua

A **cobertura de testes** mede a porcentagem do código que é executada durante os testes, ajudando a identificar áreas não testadas.
A **automação (CI/CD)** garante que os testes sejam executados de forma contínua em cada *commit* ou *pull request*.

---

### 🧩 Gerando Relatórios de Cobertura

O Dart e o Flutter possuem suporte nativo para geração de cobertura via `flutter test --coverage`.

#### 🔹 Passo 1 — Executar os testes com cobertura

```bash
flutter test --coverage
```

#### 🔹 Passo 2 — Visualizar o relatório

O comando gera a pasta `coverage/lcov.info`.
Para converter em um relatório HTML legível:

```bash
genhtml coverage/lcov.info -o coverage/html
```

Depois, abra o arquivo:

```
coverage/html/index.html
```

---

### 🧠 Interpretando a Cobertura

* **Statements Coverage** — Linhas executadas.
* **Branch Coverage** — Condições lógicas testadas.
* **Function Coverage** — Funções chamadas.
* **Class Coverage** — Classes instanciadas/testadas.

> 💡 Dica: Busque manter a cobertura acima de **80%**, mas foque em **testar o que importa**, não apenas em números altos.

---

### ⚙️ Integração Contínua (CI) no GitHub Actions

Crie um arquivo `.github/workflows/test.yml`:

```yaml
name: Flutter Tests

on:
  push:
    branches: [ main ]
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3
      - uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.16.0'

      - name: Instalar dependências
        run: flutter pub get

      - name: Rodar testes com cobertura
        run: flutter test --coverage

      - name: Upload cobertura
        uses: codecov/codecov-action@v3
        with:
          files: ./coverage/lcov.info
          flags: flutter
          name: flutter-tests
```

---

### 📦 Integração com Codecov (opcional)

1. Crie uma conta em [https://codecov.io](https://codecov.io)
2. Conecte seu repositório GitHub.
3. Adicione o token `CODECOV_TOKEN` como segredo do repositório.
4. Visualize relatórios automáticos a cada *commit*.

---

### 💡 Boas Práticas

* Automatize todos os testes antes do *merge*.
* Use **badges** no README para exibir o status dos testes e cobertura.
* Mantenha **testes rápidos e determinísticos** — nada de dependências externas lentas.
* Combine **testes unitários, de widget e de integração** na pipeline.

---

[← Testes de Integração](../08_integracao/08_integracao_pt.md) | [Referências e Recursos →](../10_referencias/10_referencias_pt.md)
