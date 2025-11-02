## **05 — Fluxo e Controle de Testes**

[← Hooks e Ciclo de Vida](../04_hooks/04_hooks_pt.md) | [Testes Assíncronos →](../06_assincronos/06_assincronos_pt.md)

# 📘 Fluxo e Controle

O **fluxo e controle** de testes em Dart e Flutter permite **gerenciar execução, pular testes, e organizar a saída de resultados** de maneira estruturada.

### ⏩ Ignorando Testes (Skip)

É possível ignorar testes individuais ou grupos inteiros usando o parâmetro `skip`:

```dart
test('Teste desativado temporariamente', () {}, skip: true);

test('Teste com razão para pular', () {}, skip: 'Funcionalidade ainda em desenvolvimento');

group('Grupo de testes ignorado', () {
  test('Este teste não será executado', () {});
}, skip: true);
```

> 💡 Ignorar um `group` faz com que todos os `test`s e hooks (`setUp`/`tearDown`) dentro dele também sejam ignorados.

### 📝 Mensagens de Descrição

A **descrição** passada para `test()` ou `group()` aparece no console e é usada para filtrar testes:

```dart
void main() {
  group('Autenticação', () {
    test('Deve permitir login com credenciais válidas', () {
      // console: "Autenticação Deve permitir login com credenciais válidas"
    });
  });
}
```

### 🔍 Executando Testes Específicos

É possível executar apenas determinados testes usando o terminal:

```bash
flutter test -n "login com credenciais válidas"
```

O parâmetro `-n` aceita **regex**, permitindo executar testes com nomes específicos.

### 🧭 Boas Práticas

* Nomeie os testes de forma **descritiva e consistente**.
* Use `skip` apenas para funcionalidades temporariamente desativadas.
* Combine `group` com descrições detalhadas para **legibilidade** do relatório.

---

[← Hooks e Ciclo de Vida](../04_hooks/04_hooks_pt.md) | [Testes Assíncronos →](../06_assincronos/06_assincronos_pt.md)
