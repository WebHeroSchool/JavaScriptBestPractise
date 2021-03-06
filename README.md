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
`getUserData` и `getUserInfo` — довольно нечеткие имена. О каких данных и какой информации идет речь?

Важно, чтобы имена наших функций, методов и переменных выражали их точное значение.

`GetUserPost` — куда лучшее имя, поскольку здесь мы точно понимаем, что извлекаем.

В случае сомнений выбирайте описательность, а не краткость
Нужно стараться быть как можно более лаконичным. Однако, если суть вашей функции двумя-тремя словами в имени не выразить, лучше описать ее большим количеством слов.

`findUserByNameOrEmail` и `setUserLoggedInTrue` лучше, чем
`findUser`.

### 7.Используйте подходящие по смыслу глаголы
Функции обычно создают, читают, обновляют или удаляют (create, read, update or delete) что-либо. Можно подойти к делу даже более тщательно, чтобы ваши функции создавали, извлекали, устанавливали, добавляли, убирали, сбрасывали и удаляли (create, get, set, add, remove, reset, delete) разные вещи.

Имя функции должно быть глаголом или фразой, содержащей глагол, и должно сообщать о том, что эта функция делает.

При этом следует быть последовательным. Т.е., для извлечения данных всегда использовать get, а не get, retrieve, return и десять тысяч других слов.

В общем, должно быть

`getQuestions, getUserPosts, getUsers, `
а не
`getQuestions, returnUsers, retrieveUsers`.
Конечно, все это вариации одних и тех же слов, но вам нужно выбрать для себя какой-то один вариант и придерживаться его постоянно. Например, когда удаляете что-нибудь, используйте или delete, или remove (но не оба слова) во всей вашей программе.

### 8. Избегайте однобуквенных имен переменных
В долгосрочной перспективе от слишком коротких имен больше хлопот, чем экономии на нажатиях клавиш.

Имена должны быть краткими и описательными. Переменная, инициализированная глобально, может в конечном итоге использоваться через сотню строк. Если она обозначается одной буквой, легко забыть, что это за переменная.
``` js
const dueDate = new Date()
```
гораздо лучше, чем
``` js
const d = new Date();
```
и
``` js
const query = () => { ... };
```
тоже гораздо лучше, чем
``` js
const q = () => { ... };
```
Однобуквенные имена можно использовать в маленьких функциях или в качестве индекса в цикле (это нормально):
``` js
for(let i = 0; i < 10>; i ++) {
  // ...
}
```

### 9. Комментируйте столько, сколько нужно, но не более.
Комментарии - это ваши сообщения другим разработчикам (и вам самому, если вы вернетесь к своему коду после нескольких месяцев работы над чем-то другим). На протяжении многих лет велись многочисленные битвы о том, следует ли вообще использовать комментарии, главный аргумент в том, что хороший код должен объяснять сам себя.

Я считаю недостатком этого аргумента то, что объяснения - вещь очень субъективная - нельзя ожидать, что каждый разработчик поймет, что делает тот или иной код, исходя из одного и того же объяснения.

Комментарии никому не повредят, если вы сделаете их правильно.
Комментарии могут находиться в любом месте скрипта. Они не влияют на его выполнение, поскольку движок просто игнорирует их.

**Однострочные комментарии начинаются с двойной косой черты //.**

Часть строки после **//** считается комментарием. Такой комментарий может как занимать строку целиком, так и находиться после инструкции.

Как здесь:
``` js
// Этот комментарий занимает всю строку
alert('Привет');

alert('Мир'); // Этот комментарий следует за инструкцией
```
**Многострочные комментарии начинаются косой чертой со звёздочкой  и заканчиваются звёздочкой с косой чертой.**

Как вот здесь:
``` js
/* Закомментировали код
alert('Привет');
*/
alert('Мир');
```

### 10. Не передавайте строку в "SetInterval" или "SetTimeOut"

**Не правельно**
``` js
setInterval(
 "document.getElementById('container').innerHTML += 'My new number: ' + i", 3000
 );
```
Этот код не только неэффективен, но и ведет себя таким же образом, как и вела бы себя функция "eval". Никогда не передавайте строку в "SetInterval" или "SetTimeOut". Вместо этого передавайте имя функции.

**Правельно**

``` js
setInterval(someFunction, 3000);
```