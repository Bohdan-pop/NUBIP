# Веб-розробка - JS: тип об'єкта та масиви

Теоретичні матеріали для самостійної підготовки студентів:

https://uk.javascript.info/object
https://uk.javascript.info/object-copy
https://uk.javascript.info/object-methods

https://uk.javascript.info/array
https://uk.javascript.info/array-methods

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

### Тест №1: Тип об'єкта:

1. Чи можете ви створити об’єкт у JS без виклику конструктора `Object`?

- ✅: Так, звичайно, ви можете використовувати фігурні дужки: {}.
- Ні, конструктор потрібно завжди використовувати.
- Так, можна використовувати квадратні дужки: [].

2. Які типи даних можна використовувати для значень властивостей об’єкта?

- Лише примітивні типи та функції.
- ✅: Всі види.
- Лише примітивні типи.

3. Чи можете ви використовувати рядок `let`, `const` і `return` як ключі об’єкта?
- ✅ Так.
- ні.
- Тільки `let` і `const`.

### Тест №2: Масиви

1. Як отримати кількість елементів у масиві?

- ✅: шляхом доступу до властивості `length`.
- За допомогою доступу до властивості `size`.
- Викликаючи метод `length()`.

2. Що робить цей код? `let numbers = new Array(1, 2, 3);`

- ✅: створюється масив із 3 елементів: `[1, 2, 3]`
- Створює масив з індексами, починаючи з `1`.
- Створює масив масивів: `[[1], [2], [3]]`.

3. Що робить цей код? `let numbers = new Array(3);`

- Він створює масив з одним елементом усередині: `[3]`
- Він просто повертає "3" замість масиву.
- ✅: створюється масив із 3 невизначених елементів.

## 2. Приклади типів об'єктів

1. **Оголошення та використання об’єктів**
> **ПИТАННЯ**: Як створити порожній об’єкт у JavaScript?
> Ми можемо захотіти використовувати об’єкти, коли хочемо зберігати дані, які якось пов’язані.

**Приклад:**

```js
console.clear();

// Перед об'єктами
let firstName = "James";
let lastName = "Jamison";

// Синтаксис об'єктів
let user = {
   firstName: "James",
   lastName: "Jamison",
   "      123": "any value",
   1: "value for a number key",

   options: {
      color: "red",
      theme: {
         //...
      },
   },
};


// Доступ до властивостей
user["language"] = "en";
console.log(user.firstName);
console.log(user["lastName"]);// квадратні дужки
console.log(user["      123"]);
console.log(user[1]);


// Видалити властивість
delete user.language;

// Властивість з непарним ключем
let propertyKey = "      123";
console.log(user[propertyKey]);


// Вбудовані об'єкти
let userOptionsColor = user.options.color;
console.log("userOptionsColor", userOptionsColor);

function sayHi(user) {
   console.log(`Hi, ${user.firstName} ${user.lastName}`);
}

sayHi(user);

console.log("--------------");


// Перебираємо ключі об'єктів
for (let key in user) {
   console.log(key, user[key]);
}


// Клонувати об'єкти
let dog = {
   name: "Rex",
   age: 1,
};

let cat = Object.assign({}, dog);
console.log(dog === cat);

let whale = Object.assign({}, dog, { name: "Billy" });
console.log(whale);

```

2. **Посилання на об’єкти та копіювання**
> **ПИТАННЯ**: Які відмінності між примітивними типами та об’єктами?

**Приклад:**

```js
console.clear();

// Копіювання значень примітивів
let i = 0;
let j = i;

j++;
j++;
console.log(`i: ${i}, j: ${j}`);

// Копіювати об'єкти
let user = { name: "Petr" };
let admin = user;

admin.name = "James Jameson";
console.log(user.name);


// Порівняти за посиланням
console.log({} === {});
console.log({} == {});

// Ми можемо змінювати властивості об'єкта навіть за допомогою const
const dog = { type: "bad" };
dog.type = "good";

console.log(dog);

// Як це впливає на наш код?
const car = { brand: "Ford" };
const car2 = car;

function change(carToChange) {
   carToChange.brand = "Toyota";
}

change(car);

console.log(car);
console.log(car2);

```

3. **методи this і object**

```js
"use strict";

console.clear();

let user = {
   name: "Batman",
   style: "",

   sayHi() {
      console.log(`Hi, I am `, this.name);
   },
   // Arrow function не має свого this
   sayBye() {
      let arrow = () => console.log("Bye from: ", this.name);

      arrow();
   },
};

let userSayBye = user.sayBye;

// "this" не прив'язане
user.sayHi(); //  Hi, I am  Batman (this: user)
user["sayHi"]();


// Видає помилку, оскільки this не зв'язано
// userSayBye(); // this: undefined

function test() {
   console.log(this);
}

test(); // this - undefined(або window) якщо не strict mode);
user.test = test;
user.test(); // this - user

```

## 3. Приклади масивів

1. **Основи роботи з масивом:**
   **Приклад**

```js
console.clear();

// 1. Створення
let names = ["Bob", "Matt", "Chuck"];

// 2. довжина
console.log(names.length);
console.log(names);

// 3. Отримати значення за рядком
console.log(names["0"]);
console.log(names[0]); // той самий результат

// 4. push, pop
names.push("Bob");
let lastElement = names.pop();

// 5. shift, unshift
names.shift(); // Видаляє 1-й елемент
names.unshift("NEW_NAME"); // Додає 1-й елемент
console.log("shift/unshift: ", names);

// 6. приєднатися
let joinedNames = names.join("|||");
console.log(joinedNames);

// 7. Ви можете помістити всередину будь-який тип і змішати різні типи
// Але, будь ласка, не змішуйте їх
let randomArray = [1, null, {}, function () {}, "string"];
console.log(randomArray);

// 8. Оператор розширення для передачі як параметра
let numbersForCheck = [1, 2, 9, 27, -5];
let max = Math.max(1, 2, 9, 27, -5); // 27

let maxSpread = Math.max(...numbersForCheck);

console.log("max: ", max, "maxSpread: ", maxSpread);

```

2. **Ітерація**
   **Приклад**

```js
console.clear();

let files = ["text.txt", "cat.jpeg", "table.xls", "contract.pdf", "salary.doc"];

for (let i = 0; i < files.length; i++) {
   console.log(files[i]);
}

console.log("-------------------------------------------");

for (let file of files) {
   console.log(file);
}

```

3. **Map і forEach**

**Приклади**

```js
console.clear();

let heroes = [
   {
      name: "Spiderman",
      type: "Small",
      powers: ["super strength", "spider sense"],
   },
   {
      name: "Hulk",
      type: "Big",
      powers: ["super strength", "self-healing"],
   },
   {
      name: "Ironman",
      type: "Medium",
      powers: ["armor", "money"],
   },
];

// 1. Отримати масив імен
// Виконайте кроки: отримати всі імена, отримати імена без героїв `type: "Small"`
let heroNames = [];
for (let hero of heroes) {
   if (hero.type !== "Small") {
      heroNames.push(hero.name);
   }
}


// 2. Те саме з методом forEach
let heroNames2 = [];
heroNames2.forEach((hero) => {
   if (hero.type !== "Small") {
      heroNames2.push(hero.name);
   }
});


// Використання Map
let heroNamesMap = heroes
        .filter((hero) => hero.type !== "Small")
        .map((hero) => hero.name);

console.log(heroNames);
console.log(heroNamesMap);


// [необов'язковий] 3. includes метод
let ironman = heroes[2];
console.log(ironman);

const hasMoney = ironman.powers.includes("money");
console.log(`hasMoney: ${hasMoney}`);
const hasSelfHealing = ironman.powers.includes("self-healing");
console.log(`hasSelfHealing: ${hasSelfHealing}`);

// [необов’язковий] 4. Array.isArray
// Цей метод більш надійний, ніж instanceof
console.log(Array.isArray(1), Array.isArray([1, 2, 3]), Array.isArray({}));

// [необов'язковий] 5. find
const expectedHero = heroes.find((hero) =>
        hero.powers.includes("super strength")
);
console.log(expectedHero); // "Spiderman": повертає перший знайдений елемент

// [необов'язково] 6. Reduce
const allThePowers = heroes.reduce((powers, hero) => {
   powers[hero.name] = hero.powers;

   return powers;
}, {});

console.log(allThePowers);

```

6. **Опис вимог до практичного завдання.**

У цій темі ми розглянули майже всю теорію, необхідну для практичного завдання, тому ми можемо пропустити додаткові пояснення.

1 **Функція "createUserWithFullName"**

Напишіть функцію `createUserWithFullName`, щоб створити об’єкт із двома властивостями, `firstName` і `lastName`, і методами `setFirstName`, `setLastName` і `getFullName`.

Ви можете використовувати функцію `createUser` із завдання `#1` як початкову.

 ```js
function createUserWithFullName(firstName, lastName) {
 // ваш код...
}
```

Ця функція приймає два параметри:
`firstName` - рядок з ім'ям користувача
`lastName` - рядок із прізвищем користувача

1. Функція повинна створити новий об’єкт і повернути його.

2. Повернений об’єкт повинен мати дві властивості: `firstName` і `lastName`. Значення для властивостей мають бути з параметрів `firstName` і `lastName`.

3. Повернений об’єкт повинен мати три методи:
   `setFirstName(newFirstName)` - приймає `newFirstName` як параметр і встановлює його значення властивості `firstName` об'єкта
   `setLastName(newLastName)` - приймає `newLastName` як параметр і встановлює його значення властивості `lastName` об'єкта
   `getFullName()` - об’єднує значення властивостей `firstName` і `lastName`, додаючи пробіл між ними та повертаючи результат

Це має працювати так само, як функція `getFullName` з попереднього завдання.

Будь ласка, зверніть увагу, що методи повинні використовувати `this` всередині.

**приклад використання функції:**
```js
let user = createUserWithFullName('Stan', 'Lee');

user.firstName; // 'Stan' 
user.lastName; // 'Lee' 

let fullName = user.getFullName(); // 'Stan Lee' 

user.setFirstName('Will');
user.setLastName('Smith');

user.firstName; // 'Will' 
user.lastName; // 'Smith' 

let fullName = user.getFullName(); // 'Will Smith' 
let emptyFullName = getFullName();
emptyFullName; // "" 

```


2 Функція "getMaxNumbers"
Напишіть функцію getMaxNumbers, яка приймає двовимірний масив чисел як параметр і повертає масив із максимальними числами з кожного вкладеного масиву.
```js
function getMaxNumbers(arr) {
 // ваш код...
}
```
Ця функція приймає один параметр: arr (двовимірний масив).
```js
const arr = [[1, 6, 9, 1], [2, 3, -4, 8], [15]];
```
1. Функція має повернути новий одновимірний масив.
2. Функція повинна зібрати максимальну кількість вкладених масивів у новий масив.
3. Крім того, функція не повинна працювати через порожній масив. У цьому випадку він повинен повернути [].
   Приклад використання функції:
```js
const arr = [[1, 6, 9, 1], [2, 3, -4, 8], [15]];
let newArrMaxNumber = getMaxNumbers(arr); // [9,8,15];
const arr = [];
let newArrMaxNumber = getMaxNumbers(arr); // [];
```

