# JavaScript best practices. :wink:

### 1.Объявление переменных
Используйте let или const для объявления переменных. Перестаньте использовать var это усторевший вариант.

**Правельно**

``` js
let userAge = "25";
```

**Не правельно**
``` js
var userAge = "25";
```

### 2.Избегайте крупных функций

Крупный размер функции или даже класса намекает на то, что эта функция делает больше, чем следовало бы. Приведенный пример может показаться простым, но он хорошо иллюстрирует проблему. Эта функция делает намного больше, чем нужно.
``` js
const addMultiplySubtract = (a, b, c) => {
  const addition = a + b + c;
  const multiplication = a * b * c;
  const subtraction = a - b - c;

  return `${addition} ${multiplication} ${subtraction}`;
}
```
Будет лучше создать несколько разных функций, чтобы разделить логику:
``` js
const add = (a, b, c) => a + b + c;
const multiply = (a, b, c) => a * b * c;
const subtract = (a, b, c) => a - b - c;
```
### 3.Используйте === вместо ==

Рекомендуется всегда использовать === при сравнении т.к. он предотвращает ошибки приведения типов.

Оператор == сравнения всегда преобразует (в совпадающие типы) перед сравнением. Оператор === заставляет сравнивать значения и тип.
**Правельно**

``` js
1 === true;
```

**Не правельно**
``` js
1 == true;
```

### 4. Eval = зло
Функция "eval" предоставляет нам доступ к компилятору JavaScript. Собственно, с ее помощью мы можем выполнить код, переданный ей в виде строки.

В результате ее использования не только значительно понизится производительность вашего скрипта, но и возникнет огромный риск, связанный с нарушением секретности (информационной безопасности), поскольку при вызове eval переданной строке предоставляются значительные полномочия (* например, могут читаться и меняться  локальные переменные). Избегайте ее использования!

### 5. Используйте {} вместо New Object()

Имеется множество способов создания объектов в JavaScript. Вероятно, более традиционным способом является использование конструктора «new», например:
``` js
let object = new Object();
 object.name = 'Niki';
 object.lastName = 'Black';
 object.someFunction = function() {
    console.log(this.name);
 }
```
Однако, этот способ зарекомендовал себя как «плохую практику» без должных на то оснований. Вместо этого рекомендуется использовать более надежный способ создания объектов – при помощи литерала (* литеральная (символьная) константа).
``` js
let object = {
    name: 'Niki',
    lastName = 'Black',
    someFunction : function() {
       console.log(this.name);
    }
 };
```

### 6. Использование осмысленных имен
**getUserData** и **getUserInfo** — довольно нечеткие имена. О каких данных и какой информации идет речь?

Важно, чтобы имена наших функций, методов и переменных выражали их точное значение.

**GetUserPost** — куда лучшее имя, поскольку здесь мы точно понимаем, что извлекаем.

В случае сомнений выбирайте описательность, а не краткость
Нужно стараться быть как можно более лаконичным. Однако, если суть вашей функции двумя-тремя словами в имени не выразить, лучше описать ее большим количеством слов.

**findUserByNameOrEmail** и **setUserLoggedInTrue** лучше, чем
**findUser**.