# Веб-розробка - JS: Примітивні типи - Умови та цикли

Теоретичні матеріали для самостійної підготовки студентів:

https://uk.javascript.info/number
https://uk.javascript.info/string
https://uk.javascript.info/primitives-methods
https://uk.javascript.info/logical-operators
https://uk.javascript.info/while-for


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

Примітивні типи:

1. Як перевірити тип даних змінної в JavaScript?
- Використання властивості dataType.
- З функцією checkType.
- ✅: використання оператора typeof.
2. Поясніть різницю між null і undefined у JavaScript.
- ✅: null: навмисна відсутність, undefined: неініціалізовано.
- null: неініціалізований, undefined: навмисна відсутність.
  — Вони однакові.
3. Що таке вихід typeof "true" у JavaScript?
- "логічний".
- «число».
- ✅: "рядок".

Умови та цикли:

1. Яке призначення оператора if-else у JavaScript?
- Оголошувати функції.
- Повторювати код нескінченно довго.
- ✅: приймати рішення на основі умов.
2. Що робить цей код: `while([умова]) { // ваш код }?`
- Виконується один раз.
- ✅: повторює код під час виконання умови.
- пропускає цикл.
3. Яке призначення оператора switch?
- Визначити функції.
- Для створення масиву.
- ✅: Кілька умовних гілок.

## 2. Теоретичні теми

1. **Динамічний набір**

- Динамічно типізовані мови – це ті (наприклад, JavaScript), у яких інтерпретатор призначає змінним тип під час виконання на основі значення змінної на той момент.

> **ПИТАННЯ**: як працює динамічний тип?

**Результат:**

```js
let foo; // foo не визначено
foo = 42; // foo тепер число
foo = "bar"; // foo тепер є рядком
foo = true; // foo тепер є логічним
```

2. **Примітивні типи**
> **ПИТАННЯ**: поясніть концепцію примітивних типів даних у JavaScript.

- примітивні типи: string, number, boolean, undefined, null, bigint, symbol
- об'єкт: об'єкт, масив, функція ... Все є об'єктом.

**Результат**:

```js
console.clear();

// ЛОГІЧНИЙ
const isAdmin = true;
const hasPermission = false;

// ЧИСЛО
const userAge = 42;
const pi = 3.14;
const binaryByte = 0b11111111;
const curentLevel = NaN;
const infinityValue = 1 / 0;
const negativeInfinity = -infinityValue;
const complexSum = 5e-14;


// STRING
const title = "title";
const subtitle = "subtitle";
const description = `description`;
const note = new String("note");


// NULL
// Відомо, що nullValue існує, але воно не має значення (значення «empty» або «nothing»)
const nullValue = null;

// НЕВИЗНАЧЕНО
let undefinedValue;
foo = undefined; // Не робіть цього. Присвоєння undefined змінній може зробити ваш код менш зрозумілим і складнішим для розуміння.

// BIGINT
const bigIntValue = 1234567890123456789012345678901234567890n;
const maxSafeInteger = Number.MAX_SAFE_INTEGER; // 9007199254740991
const minSafeInteger = Number.MIN_SAFE_INTEGER; // -9007199254740991
const largeBigInt = 2n ** 53n; // 9007199254740992n

// СИМВОЛ
const anchor = Symbol("anchor");
```

3. **тип оператора**
> **ПИТАННЯ**: як перевірити тип змінної в JavaScript? Що таке оператор typeof?

**Результат**:

```js
console.clear();

// Числа
console.log(typeof 37);
console.log(typeof 3.14);
console.log(typeof 42);
console.log(typeof Math.LN2);
console.log(typeof Infinity);
console.log(typeof NaN); // Незважаючи на те, що це "Не-число"
console.log(typeof Number("1")); // Число намагається розібрати речі в числа
console.log(typeof Number("shoe")); // включаючи значення, які не можуть бути приведені до числа

// Рядки
console.log(typeof "");
console.log(typeof "bla");
console.log(typeof `template literal`);
console.log(typeof "1"); // зауважте, що число в рядку все ще є типом рядка
console.log(typeof typeof 1); // typeof завжди повертає рядок
console.log(typeof String(1)); // Рядок перетворює будь-що в рядок, безпечнішеtoString

// Логічні значення
console.log(typeof true);
console.log(typeof false);
console.log(typeof Boolean(1)); // Boolean() перетворює значення залежно від того, правдиві вони чи хибні

// Не визначено
console.log(typeof undefined);
console.log(typeof declaredButUndefinedVariable);
console.log(typeof undeclaredVariable);

// Null
// Це існує з початку JavaScript
console.log(typeof null);

// [необов'язковий]
// Символи
console.log(typeof Symbol("foo"));

// [необов'язковий]
// Bigint
console.log(typeof 1n);
console.log(typeof BigInt("1"));
```

4. Корисні методи `"string"` і літерал шаблону
> **ПИТАННЯ**: які найкорисніші рядкові методи?

**Результат**:

```js
console.clear();

// Корисні рядкові методи
const browserType = "Mozilla";
browserType.length; // 7
browserType.indexOf("M"); // 0
browserType.includes("ill"); // правда
browserType.split(""); // ["M", "o", "z", "i", "l", "l", "a"]
browserType.toUpperCase(); // 'MOZILLA'
" M oz ill a ".trim(); // 'M oz ill a';

// [необов'язковий]
browserType.concat(" browser"); // 'Браузер Mozilla'
browserType.replace("Mo", "God"); // Godzilla
browserType.charAt(1); // "o"
browserType[0]; // "M"
browserType.slice(1, 3); // oz
browserType.substring(1, 3); // oz

// Літерали шаблону
let firstName = "John";
let lastName = "Doe";

let fullNameBeforeStringLiterals = "Full name is: " + firstName + " " + lastName;
let fullName = `Full name is: ${firstName} ${lastName}`; // Full name is: John Doe

console.log(fullNameBeforeStringLiterals);
console.log(fullName);

```

5. **умовні оператори:**
> **ПИТАННЯ**: Які умовні висловлювання ви знаєте?

**Результат:**

```js
console.clear();

// оператор if-else
function checkNumberTypeIf(number) {
  if (number > 0) {
    return "Positive";
  } else if (number < 0) {
    return "Negative";
  } else {
    return "Zero";
  }
}


const positiveNumber = 42;
const result1 = checkNumberTypeIf(positiveNumber);
console.log(`The number is ${result1}`); // The number is Positive

// Тернарний оператор
console.clear();
function checkNumberTypeTernary(number) {
 // важко передбачити результат з першого погляду з вкладеним тернарним оператором
  const result = number > 0 ? "Positive" : number < 0 ? "Negative" : "Zero";
  return result;
}

const negativeNumber = -24;
const result2 = checkNumberTypeTernary(negativeNumber);
console.log(`The number is ${result2}`); // The number is Negative

// swith case
function checkDayType(day) {
  switch (day) {
    case "Saturday":
    case "Sunday":
      return "Weekend";
    default:
      return "Weekday";
  }
}

const day = "Friday";
const result = checkDayType(day);
console.log(`${day} is a ${result}`); // Friday is a Weekday

// [необов'язковий]
// Використовуйте нульовий оператор об’єднання, щоб надати значення за замовчуванням.
let defaultValue = null;
let providedValue = defaultValue ?? "Default Value";
console.log(`Value: ${providedValue}`); // Value: Default Value

```

6. **Логічні оператори**
> **ПИТАННЯ**: Які логічні оператори ви знаєте?

**Результат:**

```js
console.clear();

// Яка різниця?
console.log("1 == true", 1 == true);
console.log("1 === true", 1 === true);

// Logical "AND" "OR" "NOT"
let hour = 9;

if (hour < 10 || hour > 18) {
  console.log("Office is closed.");
}

// Logical "OR", "AND"
console.log(false || true);
console.log(false && true);

// Logical "NOT"
console.log(!false);
console.log(!true);
console.log(typeof !!1); // два виклики ! (логічний оператор НІ) еквівалентний Boolean()

console.log(3 && 5);
console.log(3 && 5 && null && 8);
console.log(null || 0);
console.log(0 || (1 && 2) || 3);

const example1 = true || console.log("You don't see this text");
const example2 = false && console.log("This too");

```

7. **Цикли:**
> **ПИТАННЯ**: які цикли ви знаєте в JS?

**Результат:**

```js
console.clear();

// for Цикл
for (let i = 0; i < 5; i++) {
  console.log(`Iteration ${i}`);
}
// while Цикл
let count = 0;
while (count < 5) {
  console.log(`Count: ${count}`);
  count++;
}

// do-while Цикл
let num = 1;
do {
  console.log(`Number: ${num}`);
  num++;
} while (num <= 5);


// [необов'язковий]
// Використовуйте цикл do-while для читання введених даних, доки користувач не введе «quit».
// let userInput;
// do {
//   userInput = prompt('Enter something (or "quit" to exit):');
//   console.log(`You entered: ${userInput}`);
// } while (userInput !== 'quit');


// [необов'язковий]
// Використання вкладених циклів для створення шаблону.
for (let i = 1; i <= 5; i++) {
  let pattern = "";
  for (let j = 1; j <= i; j++) {
    pattern += "* ";
  }
  console.log(pattern);
}


// [необов'язковий]
// Цикл через рядок
function countVowels(sentence) {
  let vowelCount = 0;
  const vowels = "aeiouAEIOU";

  for (let char of sentence) {
    if (vowels.includes(char)) {
      vowelCount++;
    }
  }

  return vowelCount;
}

const sentence = "This is a sample sentence.";
const result = countVowels(sentence);
console.log(`Number of vowels in the sentence: ${result}`);

```

8. **Опис вимог до практичного завдання.**



1. **Функція "countChars"**

Напишіть функцію `countChars` для підрахунку символів у рядку, але без пробілів на початку та в кінці.
```js
function countChars(str) {
 // ваш код...
}
```

Ця функція приймає один параметр, `str`, рядок для підрахунку символів.
1. Функція має повернути кількість символів у переданому рядку `str`.
2. Він не повинен рахувати пробіли на початку та в кінці рядка.
3. Якщо рядок складається лише з пробілів, `countChars` має повернути `0`.

**Приклад використання функції:**
```js
countChars(' '); // 0, рядок складається лише з пробілів
countChars('Теодор'); // 6, рядок складається з 6 символів
countChars(' Сем '); // 3, ми рахуємо все, крім пробілів
```

4. **Функція "formatMoney"**

Напишіть функцію `formatMoney`, яка приймає число та повертає форматоване рядкове значення, схоже на `$100.00`.
```js
function formatMoney(amount) {
  // your code...
}

```

Ця функція приймає один параметр, `amount`, суму грошей для форматування.
1. Функція повинна працювати як з цілими числами, так і з дробами.
2. В отриманому рядку після крапки завжди має бути два символи. Щоб округлити до двох символів, використовуйте спеціальний метод, доступний для чисел `toFixed(2)`. Ви можете прочитати більше про це тут: [toFixed MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed).

**Приклад використання функції:**
```js
formatMoney(100); // "$100.00"
formatMoney(100.889); // "$100.89"
```


5. **Функція "convertToBoolean"**

Напишіть функцію `convertToBoolean`, яка має приймати будь-яке значення примітивного типу та перетворювати його на `boolean`.
```js
function convertToBoolean(value) {
  // your code...
}

```
Ця функція приймає один параметр: `value` — будь-яке значення типу `number`, `string`, `boolean`, `null` або `undefined`.
Ця функція має перетворити `value` на тип `boolean`.

**Приклад використання функції:**
```js
convertToBoolean(100); // true
convertToBoolean(true); // true
convertToBoolean('Some cool string'); // true
convertToBoolean(null); // false
convertToBoolean(undefined); // false

```