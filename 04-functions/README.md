# Веб-розробка - JS: Функції

https://uk.javascript.info/advanced-functions
## Вступ

1. Лектор запитує, як пройшов перший тиждень навчання, і отримує відповідь за допомогою «Ментиметра» або просто в чаті.
2. Лектор описує план заняття:
- `Формат`: приклади кодування в реальному часі.
- `Тривалість`: до 1,5 годин, з 5-хвилинною перервою посередині.
- `Питання`: пишіть свої запитання в чат зустрічі під час сесії, лектор відповість на них під час сесії.
- `Домашнє завдання/практичне завдання`: наприкінці заняття ми поговоримо про практичне завдання, представимо та відповімо на запитання, пов’язані з ним.

## 1. Тест у Mentimeter на тему:

Ми починаємо з тесту, щоб зрозуміти, чи вони вже щось навчилися/знають.

**Ви можете знайти тест Mentimeter тут:**

https://www.mentimeter.com/app/presentation/

**Умовні позначки:**

- ✅: правильна відповідь
- [необов’язково]: необов’язкова тема, запитання або приклад коду. Це залежить від відповідей учнів, та кількості доступного часу.

**Питання:**

Функції:

1. Як оголосити функцію-стрілку з іменем "sum" з параметрами a і b.

   - function sum(a, b) {}
   - const sum = function(a, b) {}
   - ✅: const sum = (a, b) => {}

2. Різниця між function expressions and declarations?

- ✅: Declarations вспливають; вирази ні.
- Expressions вспливають; декларації ні.
- Різниці нема.

3. Що означає термін NFE в контексті функцій?

    - Not Found Error.
    - ✅: Named Function Expression.
    - New Function Execution.

4. Яка різниця між call() і apply() у JavaScript.

- ✅: call() передає аргументи окремо; apply() передає масив.
- call() передає масив; apply() передає аргументи окремо.
  — Обидва способи взаємозамінні.

5. Призначення bind() у JavaScript?
- Створення функцій.
- ✅: прив’язати функцію до об’єкта.
- Застосовувати стилі.

## 2. Теоретичні теми

1. **Основи роботи**

> **ПИТАННЯ**: які є різні способи визначення функції в JavaScript?

**Результат:**

```js
// Оголошення функції - Function Declaration
function greet(name) {
  return `Hello, ${name}!`;
}

// Вираз функції - Function Expression
const greetExpression = function (name) {
  return `Hello, ${name}!`;
};

// Функція стрілки - Arrow Function
const greetArrow = (name) => `Hello, ${name}!`;
```

2. **Параметри, аргументи та значення, що повертається**

> **ПИТАННЯ**: Запитання: Поясніть поняття параметрів функції.

**Результат**:

```js
console.clear();

function addNumbers(a, b) {
   return a + b;
}

const result = addNumbers(3, 5);
console.log(`The sum is: ${result}`);
```

3. **Функція як об’єкт**
> **ПИТАННЯ**: функція є об’єктом? Яку спільну функцію та предмет мають? Що відрізняється?

**Результат**:

```js
console.clear();

function multiply(a, b) {
   return a * b;
}

multiply.description = "A function to multiply two numbers.";
multiply.logResult = function (a, b) {
   console.log(`Result of multiplication: ${this(a, b)}`);
};

console.log(multiply(2, 4));
multiply.logResult(3, 5);
console.log(multiply.description);

// Посилання на multiply призначається sameMultiply. Обидві змінні стосуються однієї функції.
const sameMultiply = помножити;
sameMultiply.logResult(4, 2);

// що повертає цей код?
console.log((() => {}) == (() => {}));
console.log((() => {}) === (() => {}));
```

4. **Області функцій**
> **ПИТАННЯ**: що таке концепція області видимості у функціях JavaScript?

**Результат**:

```js
console.clear();

const globalVar = "I am global!";

function scopeExample() {
   const localVar = "I am local!";

   console.log(globalVar);
   console.log(localVar);
}

scopeExample();
// console.log(localVar); // Цей рядок призведе до помилки.
```

5. **Довжина функції та аргументи**
> **ПИТАННЯ**: що таке властивість функції length і як можна працювати з різною кількістю аргументів?

**Результат:**

```js
console.clear();

function exampleFunction(a, b, ...rest) {
   console.log(`Arguments: ${a}, ${b}`);
   console.log(`Additional arguments: ${rest}`);
   console.log(`Function length: ${exampleFunction.length}`);
}

exampleFunction(1, 2, 3);
exampleFunction(1, 2, 3, 4, 5);
```

6. **Декоратори: зв'язати, викликати, застосувати**
> **ПИТАННЯ**: поясніть поняття зв’язування, виклику та застосування у функціях JavaScript.

**Результат:**

```js
const user = {
   firstName: "John",
   lastName: "Doe",
};

function greetUser(greeting) {
   console.log(`${greeting}, ${this.firstName} ${this.lastName}!`);
}

// що поверне ця функція?
greetUser();

const boundFunction = greetUser.bind(user, "Welcome");  // повертає "зв'язану" функцію
boundFunction(); // зробити виклик із "прив'язаним" контекстом

greetUser.call(user, "Hello"); // зробити виклик із контекстом
greetUser.apply(user, ["Hi"]); // зробити виклик із контекстом

// ===================

const anotherUser = {
   firstName: "John",
   lastName: "Lennon",
};
const secondBoundFunction = boundFunction.bind(anotherUser, "Hi");  // ! не зв’язуватиме іншого користувача. Bind можна використовувати лише один раз. Замість цього буде використовуватися користувач.
const anotherBoundFunction = greetUser.bind(anotherUser, "Hi");
secondBoundFunction(); // Ласкаво просимо, Джон Доу!
anotherBoundFunction(); // Привіт, Джон Леннон!
```

7. **Функція, передана як значення**
> **ПИТАННЯ**: Як передати функцію як значення іншій функції?

**Результат:**

```js
console.clear();

function operate(a, b, operation) {
   return operation(a, b);
}

// Функція додавання двох чисел
function add(a, b) {
   return a + b;
}

// Функція віднімання двох чисел
function subtract(a, b) {
   return a - b;
}

console.log(operate(5, 3, add)); // Результат: 8
console.log(operate(5, 3, subtract)); // Результат: 2
```

7. **Оператор поширення у функціях**
> **ПИТАННЯ**: як використовувати оператор поширення (spread) (...) у функціях?

**Результат:**

```js
console.clear();

// Функція з оператором поширення
function concatenateStrings(...args) {
   return args.join(" ");
}

const result = concatenateStrings("JavaScript", "is", "fun");
console.log(result); // Result: JavaScript is fun
```

7. **Деструктуризація параметрів функції**
> **ПИТАННЯ**: як використовувати деструктуризацію в параметрах функції?

**Результат:**

```js
console.clear();

// Функція з деструктуруванням
function printUser({ firstName, lastName, age }) {
   console.log(`Name: ${firstName} ${lastName}, Age: ${age}`);
}

const user = {
   firstName: "John",
   lastName: "Doe",
   age: 25,
};

printUser(user);
```

7. **Вираз іменованої функції - Named Function Expression (NFE)**
> **ПИТАННЯ**: що таке вираз іменованої функції та як воно використовується?

**Результат:**

```js
console.clear();

const factorial = function calculateFactorial(n) {
   if (n <= 1) {
      return 1;
   } else {
      return n * calculateFactorial(n - 1);
   }
};

// Використання виразу іменованої функції
const result = factorial(5);
console.log(`Factorial of 5 is: ${result}`);
```

8. **Опис вимог до практичного завдання.** Подробиці дивіться в [DISCLAIMER.md](../DISCLAIMER.md).