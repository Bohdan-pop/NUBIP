# Веб-розробка – JS: класи та модулі JS + дата та методи JavaScript

https://uk.javascript.info/classes
https://uk.javascript.info/modules
https://uk.javascript.info/date

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

## 1. Тест у Ментиметрі на тему:

Ми починаємо з вікторини, щоб зрозуміти, чи вони вже щось навчилися/знають.

**Ви можете знайти вікторину Mentimeter тут:**

- Група 1:

**Умовні позначки:**

- ✅: правильна відповідь
- [необов’язково]: необов’язкова тема, запитання або приклад коду. Це залежить від відповідей учнів. Якщо вони вже це
  знають, ви можете пропустити це.

**Тест:**

Класи та модулі JS:

1. Чи потрібно використовувати «new» під час використання класу JS?

- ✅: Так, інакше була б помилка.
  – Ні, це не так, «new» є лише з історичних причин.
  — Так, але якщо пропустити, нічого не станеться.
  – Ні, але без «new» класи працюють інакше.

2. Що потрібно зробити, щоб використовувати модулі JS у браузері?

- Просто використовуйте "import/export" у коді.
- ✅: додайте атрибут "type="module" до тегу script.
- Ви не можете використовувати модулі JS у браузері.
- Додайте атрибут "async" або "type="module" до тегу script.

3. На що саме посилається «this» у конструкторі класу, коли використовується клас?

- ✅: До новоствореного об’єкта.
- До самого класу для додавання статичних методів.
- До новоствореного об’єкта, якщо використовується «new», до «null», якщо ні.

4. Як отримати поточну дату?

  - ✅: new Date();
  - new Date(0);
  - ✅: Date.now();
  - Date.currentDate();

5. Що робить цей код: "let date = new Date(2023);"?

— Створює об’єкт дати для 1 січня 2023 року
- ✅: створює об’єкт дати для 2023 мілісекунд, що минули з 01.01.1970
- Виникає помилка, ви повинні надати решту компонентів дати.

6. Що повертає цей код: "typeof (new Date())"?

  - ✅: "object"
  - "date"
  - "object Date"
  - "[object Object]"

## 2. Теоретичні теми

1. **Конструктор функції та клас**

> **ПИТАННЯ**: Чи є альтернатива класам JS?

**Результат:**

```js
console.clear();
let book1 = {
  title: "Sapiens: A Brief History of Humankind",
  author: "	Yuval Noah Harari",
  year: 2014,
};

let book2 = {
  title: "Harry Potter and the Deathly Hallows",
  author: "J.K. Rowling",
  year: 2007,
};

function BookFunction(title, year) {
  this.title = title;
  this.year = year;

  this.printTitle = function () {
    // У цього підходу є недоліки, але наразі це добре
    console.log(`You are reading: ${this.title}`);
  };
}

let book3 = new BookFunction("Book3", 33);
let book4 = new BookFunction("Book4", 44);

book3.printTitle();
book4.printTitle();

console.log(book3, book4);

class BookClass {
  constructor(title, year) {
    this.title = title;
    this.year = year;
  }

  printTitle() {
    console.log(`You are reading: ${this.title}`);
  }
}

const book5 = new BookClass("Book 5", 1999);
const book6 = new BookClass("Book 6", 1996);
book5.printTitle();
book6.printTitle();

console.log(book5.printTitle === book6.printTitle); // true: та сама функція зберігається в прототипі
```

2. **Синтаксис класу: приватні властивості, getter/setter**

> **ПИТАННЯ**: чи є альтернатива класам JS?

```js
console.clear();

class Book {
  #privateYear = 0;

  constructor(title) {
    this.title = title;
  }

  setYear(newYear) {
    if (Number.isFinite(newYear)) {
      this.publicYear = newYear;
    }
  }

  set year(newYear) {
    if (Number.isFinite(newYear)) {
      this.#privateYear = newYear;
    }
  }

  get year() {
    return this.#privateYear;
  }
}

const book = new Book("The Lost Symbol");

book.setYear(2010);
book.year = 2020;

console.log(book);
console.log(book.year);
```

3. **Extends Classes, instanceof**

```js
console.clear();

class Book {
  #privateYear = 0;

  constructor(title) {
    this.title = title;
  }

  setYear(newYear) {
    if (Number.isFinite(newYear)) {
      this.publicYear = newYear;
    }
  }

  set year(newYear) {
    if (Number.isFinite(newYear)) {
      this.#privateYear = newYear;
    }
  }

  get year() {
    return this.#privateYear;
  }
}

class FictionBook extends Book {
  #plot = "";

  constructor(title) {
    super(title);

    this.#plot = "Aliens are really humans but in space suits";
  }

  showPlot() {
    console.log(this.#plot);
  }

  setYear(newYear) {
    console.log("I am about to set year");
    this.lastYearTimeSet = new Date();

    super.setYear(newYear);
  }
}

const fictionBook = new FictionBook("Space Odissey 2001");
fictionBook.showPlot();
fictionBook.year = 2001;

fictionBook.setYear(2003);

console.log(fictionBook);

// instanceof
const regularBook = new Book("Winnie-the-Pooh");

console.log(regularBook instanceof Book);
console.log(fictionBook instanceof Book);
console.log(fictionBook instanceof FictionBook);
```

4. **Модулі JS**
> **ПИТАННЯ**: чи можна використовувати модулі JS безпосередньо в браузері?

Для цих прикладів потрібен контроль над додаванням сценарію до HTML.
Ми пропонуємо використовувати [CodeSandbox](https://codesandbox.io/) або [Plunker](https://plnkr.co/)

Наш приклад:
https://codesandbox.io/s/cranky-stallman-29vh2w

**Початкова структура файлів**

```баш
index.js
index.html
```

**index.html ЗРАЗОК:**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Home Page</title>
    <meta charset="UTF-8" />
  </head>

  <body>
    <div id="app"></div>
  </body>
</html>
```

**index.js SAMPLE:**

```js
document.getElementById("app").innerHTML = `
<h1>Hello, I am a bookshelf!</h1>
<h2>${bookshelfHeading}</h2>
<div>
  ${booksString}
</div>
`;
```

**index.html RESULT:**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Parcel Sandbox</title>
    <meta charset="UTF-8" />
  </head>

  <body>
    <div id="app"></div>

    <!-- ADDED SCRIPT WITH TYPE MODULE -->
    <script src="./index.js" type="module"></script>
  </body>
</html>
```

**index.js RESULT:**

```js
import Book from "./Book.js";
import { booksData, bookshelfHeading } from "./books.js";

let books = booksData.map((book) => {
  const bookObject = new Book(book.title);
  bookObject.year = book.year;
  bookObject.author = book.author;

  return bookObject;
});

let booksString = books
  .map((book) => {
    return `${book.title} by ${book.author}`;
  })
  .join("; ");

document.getElementById("app").innerHTML = `
<h1>Hello, I am a bookshelf!</h1>
<h2>${bookshelfHeading}</h2>
<div>
  ${booksString}
</div>
`;
```

**Added files**

```bash
books.js
Book.js
index.js
index.html
```

**Book.js RESULT:**

```js
class Book {
  constructor(title) {
    this.title = title;
  }

  setYear(newYear) {
    if (Number.isFinite(newYear)) {
      this.publicYear = newYear;
    }
  }

  set year(newYear) {
    if (Number.isFinite(newYear)) {
      this._privateYear = newYear;
    }
  }

  get year() {
    return this._privateYear;
  }
}

export default Book;
```

**book.js RESULT:**

```js
export const booksData = [
  {
    title: "In Search of Lost Time",
    author: "Marcel Proust",
    year: 1913,
  },
  {
    title: "Ulysses",
    author: "James Joyce",
    year: 1904,
  },
  {
    title: "Moby Dick",
    author: "Herman Melville",
    year: 1851,
  },
];

export const bookshelfHeading = "The Best Books Ever";
```

5. **Дата та методи**
> **ПИТАННЯ**: Чи є у браузері вбудовані інструменти для роботи з датами?

```js
console.clear()

// Створення
let date = new Date();
console.log(date);
console.log(date.getTime());

// Створення дати з мілісекунд
let initialDate = new Date(0);
let someDate = new Date(777777777777);
console.log(initialDate);
console.log(someDate);

// Створення дати з кожного компонента
// new Date(year, month, date, hours, minutes, seconds, ms)
let dateByEachComponent = new Date(2020, 1, 2);
console.log(dateByEachComponent);

// Доступ до компонентів дати
console.log("===== Access Date Components =====");
console.log(date.getFullYear());
console.log(date.getMonth()); // 0 11
console.log(date.getDate());
// getHours(), getMinutes(), getSeconds(), getMilliseconds()
console.log(date.getMinutes());

// Те ж саме з набором
date.setFullYear(1999);

// Отримати день тижня
let dayOfWeek = date.getDay();
console.log("dayOfWeek: ", dayOfWeek); // 0: Sunday, 6: Saturday

// Наведені вище методи повертають компоненти відносно місцевого часового поясу.
// година у вашому поточному часовому поясі
console.log(date.getHours());
// година в часовому поясі UTC+0 (Лондонський час без переходу на літній час)
console.log(date.getUTCHours());

// Отримати час у мілісекундах від дати початку
console.log(date.getTime())

// Дата виправляється сама
date = new Date(2017, 0, 36);
console.log(date);
date.setDate(129);
console.log(date);

// Аналіз дати
let dateISOString = date.toISOString();
console.log("dateISOString: ", dateISOString);
let ms = Date.parse("2012-01-26T13:51:50.417-07:00");
console.log("ms: ", ms);
let newDate = new Date(ms);
```

6. **Опис вимог до практичного завдання.** Подробиці дивіться в [DISCLAIMER.md](../DISCLAIMER.md).