# JavaScript best practices. :wink:

### 1.Объявление переменных
Используйте let или const для объявления переменных. Перестаньте использовать var это усторевший вариант.

**Правельно**

```
let userAge = "25";
```

**Не правельно**
```
var userAge = "25";
```

### 2.Избегайте крупных функций

Крупный размер функции или даже класса намекает на то, что эта функция делает больше, чем следовало бы. Приведенный пример может показаться простым, но он хорошо иллюстрирует проблему. Эта функция делает намного больше, чем нужно.
```
const addMultiplySubtract = (a, b, c) => {
  const addition = a + b + c;
  const multiplication = a * b * c;
  const subtraction = a - b - c;

  return `${addition} ${multiplication} ${subtraction}`;
}
```
Будет лучше создать несколько разных функций, чтобы разделить логику:
```
const add = (a, b, c) => a + b + c;
const multiply = (a, b, c) => a * b * c;
const subtract = (a, b, c) => a - b - c;
```