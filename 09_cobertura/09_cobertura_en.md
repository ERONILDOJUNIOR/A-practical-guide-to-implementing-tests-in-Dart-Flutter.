## **09 — Coverage and CI/CD Automation**

[← Integration Testing](../08_integracao/08_integracao_en.md) | [References and Resources →](../10_referencias/10_referencias_en.md)

# 📘 Test Coverage and Continuous Integration

**Test coverage** measures how much of your code runs during tests, helping identify untested areas.
**Automation (CI/CD)** ensures that tests run automatically on every commit or pull request.

---

### 🧩 Generating Coverage Reports

Dart and Flutter natively support test coverage generation with `flutter test --coverage`.

#### 🔹 Step 1 — Run tests with coverage

```bash
flutter test --coverage
```

#### 🔹 Step 2 — View the report

This creates a `coverage/lcov.info` file.
To convert it into an HTML report:

```bash
genhtml coverage/lcov.info -o coverage/html
```

Then open:

```
coverage/html/index.html
```

---

### 🧠 Understanding Coverage

* **Statements Coverage** — Lines executed.
* **Branch Coverage** — Logical conditions tested.
* **Function Coverage** — Functions invoked.
* **Class Coverage** — Classes tested or instantiated.

> 💡 Tip: Aim for **80%+ coverage**, but focus on **meaningful tests**, not just high numbers.

---

### ⚙️ Continuous Integration with GitHub Actions

Create a `.github/workflows/test.yml` file:

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

      - name: Install dependencies
        run: flutter pub get

      - name: Run tests with coverage
        run: flutter test --coverage

      - name: Upload coverage
        uses: codecov/codecov-action@v3
        with:
          files: ./coverage/lcov.info
          flags: flutter
          name: flutter-tests
```

---

### 📦 Integration with Codecov (optional)

1. Create an account on [https://codecov.io](https://codecov.io)
2. Connect your GitHub repository.
3. Add the `CODECOV_TOKEN` as a repository secret.
4. Get automatic coverage reports for each commit.

---

### 💡 Best Practices

* Automate all tests before merging.
* Use **badges** in your README to display test and coverage status.
* Keep **fast, deterministic tests** — avoid external dependencies.
* Combine **unit, widget, and integration tests** in your pipeline.

---

[← Integration Testing](../08_integracao/08_integracao_en.md) | [References and Resources →](../10_referencias/10_referencias_en.md)
