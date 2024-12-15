# Веб-розробка - Додатки JS і введення в DOM

https://uk.javascript.info/currying-partials
https://uk.javascript.info/map-set

https://uk.javascript.info/browser-environment
https://uk.javascript.info/dom-nodes
https://uk.javascript.info/dom-navigation
https://uk.javascript.info/searching-elements-dom

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
1. Чим об’єкт Map відрізняється від об’єкта за типами ключів?

- Приймає лише рядки.
- ✅: приймає будь-який тип даних.
- Обмежено цифрами.

2. Як об’єкт Set обробляє повторювані значення?

- ✅: Видаляє дублікати.
- Додати дублікати.
- Видає помилку.

3. Поясніть термін «мемоізація» в контексті функцій JavaScript.

- Повертає результат як об'єкт.
- Використання анонімних функцій.
- ✅: Кешування обчислених результатів.

4. Як деревоподібна структура DOM представляє елементи HTML на веб-сторінці?

- Як плоский список.
- ✅: Як ієрархічна структура.
- Як вкладені масиви елементів.

5. Яке основне призначення глобального об’єкта Document у DOM?

— Доступ до стилів CSS.
- ✅: представлення всього документа HTML.
- Зберігання функцій і тексту JavaScript.

6. Чим метод querySelector відрізняється від getElementById у виборі елементів у DOM?
- ✅: querySelector дозволяє використовувати більш гнучкі селектори у стилі CSS.
- getElementById дозволяє використовувати більш гнучкі селектори у стилі CSS;
  — Обидва способи однакові.

## 2. Теоретичні теми

1.  **Map, Set**

> **ПИТАННЯ**: які відмінності між Map і Set у JavaScript? Наведіть приклади вживання.

**Результат:**

```js
// Map — це набір пар ключ-значення, де ключі можуть мати будь-який тип даних.
// Це дозволяє легко вставляти, отримувати та видаляти елементи.
const mapExample = new Map();
mapExample.set("key1", "value1");
mapExample.set("key2", "value2");
mapExample.set(1, "value3");
mapExample.set({}, "value5");
mapExample.set(true, "value6");

console.log(mapExample.get("key1")); // value1
mapExample.get({}); // що буде в консолі?

mapExample.delete("key2");

mapExample.forEach((value, key) => {
  console.log(`${key}: ${value}`);
});

// Set — це набір унікальних значень, які автоматично усувають дублікати.
// Це корисно, коли вам потрібно зберегти список окремих елементів.
const arrayWithDuplicates = [1, 1, 2, 2, 3, 3, 4, 4, 5, 5];
const setFromDuplicates = new Set(arrayWithDuplicates);
console.log(setFromDuplicates); // Set(5) { 1, 2, 3, 4, 5 }

// Додавання значень
setFromDuplicates.add(6);
// Видалення значення
setFromDuplicates.delete(1);
// Перевірка наявності значення
console.log(setFromDuplicates.has(2));
// Ітерація значень
setFromDuplicates.forEach((value) => {
  console.log(value);
});

// [необов'язковий]
// WeakMap схожий на Map, але дозволяє лише об’єкти як ключі.
// Він містить «слабкі» посилання на ключі, що означає, що він не перешкоджатиме збиранню сміття (garbage-collected) ключів.
let weakmapExample = new WeakMap();
const objKey = {};
weakmapExample.set(objKey, "value for objKey");

// [необов'язковий]
// WeakSet схожий на WeakMap, але призначений для зберігання унікальних об’єктів.
// Він приймає лише об’єкти та містить «слабкі» посилання, що дозволяє ефективніше керувати пам’яттю.
let weaksetExample = new WeakSet();
const obj = {};
weaksetExample.add(obj);
```

2. **Chaining, Currying**

> **ПИТАННЯ**: Питання: поясніть поняття ланцюжок, каррівання (Chaining, Currying) функції.

**Результат**:

```js
console.clear();

// Каррування Currying
// Каррування — це техніка функціонального програмування, де функція має кілька аргументів
// перетворюється на послідовність функцій, кожна з яких приймає один аргумент.

function simpleAdd(x, y, z) {
  return x + y + z;
}

function curryAdd(x) {
  return function (y) {
    return function (z) {
      return x + y + z;
    };
  };
}


// Створення карірованої функції
const curriedAdd = curryAdd(1)(2); // x + y + z => 1 + 2 + z

// Застосування функції каріювання
console.log(curriedAdd(3));// Output: 6

// Ланцюжок - Chaining
// Ланцюжок можна використовувати для aпослідовність методів.
// Кожен метод повертає об’єкт, що дозволяє об’єднати виклики в один оператор.
const add = (x, y, z) => x + y + z;
// Ланцюжок методів
const result = add(1, 2, 3)
 .toString() // Перетворення результату на рядок
 .concat(" is the sum") // Об'єднання рядка
 .toUpperCase(); // Перетворити весь рядок у верхній регістр

console.log(result); // Output: "6 IS THE SUM"

// Опціональне з’єднання
const user = {
  id: 1,
  username: "john_doe",
  personalInfo: {
    name: "John Doe",
    address: {
      city: "New York",
      zipCode: "10001",
    },
  },
};

const newUser = {
  id: 2,
  username: "new_user",
  personalInfo: null,
};

// Використання Опціонального ланцюжка для безпечного доступу до вкладених властивостей
let cityName;
cityName = user?.personalInfo?.address?.city; // 'New York'
cityName = newUser?.personalInfo?.address?.city; // undefined
//cityName = newUser.personalInfo.address.city;   // TypeError: Cannot read property 'address' of null

// [необов'язковий]
// Запам'ятовування Memoization
// Запам’ятовування – це метод оптимізації, коли результат функції кешується на основі її вхідних параметрів.
// Якщо функція знову викликається з тими ж параметрами, замість повторного обчислення повертається кешований результат.

const memoizedAdd = () => {
  let cache = {};
  return (x) => {
    if (cache[x]) {
      console.log("Fetching from cache");
      return cache[x];
    } else {
      console.log("Calculating result");
      const result = x + 10;
      cache[x] = result;
      return result;
    }
  };
};


// Створення мемоізованої функції
const memoAdd = memoizedAdd();

// Використання мемоізованої функції з тим самим входом
console.log(memoAdd(5)); // Output: Calculating result  | 15

// Отримання результату з кешу, оскільки введення є тим самим
console.log(memoAdd(5)); // Output: Fetching from cache | 15
```

### Вступ до прикладів DOM

**Використовуйте ці HTML і CSS для наступних практик DOM:**

```html
<h1
        someNonStandardAttribute="I am non standard attirbute"
        class="some class names active"
        data-name="some_useful_value"
        data-one-more="44"
>
  Document Title
</h1>

<a href="/some_url" id="title">Link text we will erase</a>

<div>Regular div without class name <span>Nested span</span></div>
<div class="second-div">This text will remain</div>

<div class="parent-element">
  I am parent
  <div class="child-element">
    I am nested
    <div class="sub-child-element">I am also nested but more</div>
  </div>
</div>
```

```css
.parent-element {
  display: inline-block;
  padding: 10px;
  margin-top: 10px;
  border: 3px dashed #bada55;
}

.child-element {
  padding: 10px;
  border: 3px solid red;
}

.sub-child-element {
  padding: 10px;
  border: 3px solid green;
}
```

3. **Навігація та пошук у DOM**
> **ПИТАННЯ**: як ми можемо переміщатися по дереву DOM?
> **ПИТАННЯ**: як ми можемо шукати елемент у js?

```js
console.clear();

// !!!!! Змінні з цього прикладу використовуються в прикладах нижче
// !!!!! Будь ласка, скопіюйте їх під час кодування в реальному часі

// Навігація елементів
let body = document.body;
// firstElementChild: отримує доступ до першого дочірнього елемента батьківського.
let firstElementChild = body.firstElementChild;
let previousElementSibling = firstElementChild.nextElementSibling; // previousElementSibling
// parentElement: отримує доступ до батьківського елемента поточного елемента.
let parentElement = previousElementSibling.parentElement;
let children = body.children;  // дочірні елементи
let childNodes = body.childNodes; // елементи дочірніх вузлів

// Пошук елементів
let h1 = document.querySelector("h1");
let div = document.querySelectorAll("div");
let a = document.getElementById("title");
let secondDiv = document.querySelector("div.second-div");

let subChildDiv = document.querySelector(".sub-child-element");
let parentDiv = subChildDiv.closest(".parent-element");

console.log(parentDiv);
```

4. **Маніпуляції з елементами DOM**
> **ПИТАННЯ**: що таке вузол DOM? Як ми можемо створити вузли DOM? Як ми можемо видалити вузли dom?

**Результат**:

```js
console.clear();

// Створення елемента
// Визначення: вузол елемента представляє елемент HTML у DOM.
// Відповідає тегам у HTML (наприклад, <div>, <p>, <a>).
// Використання: дозволяє створювати елементи HTML на вашій веб-сторінці та керувати ними.
// Приклад: цей рядок коду створює новий елемент <div> і зберігає його в змінній newElement.
let span = document.createElement("span");
console.log(span.tagName);
span.id = "some-span";
span.textContent = "Regular text";
console.log(span);

// Вставка елемента
h1.append(span); // before() after() prepend*()
h1.insertAdjacentHTML("afterbegin", '<span style="color: #bada55;">★</span>');
// Визначення: метод видалення видаляє вузол із DOM.
// Використання: дозволяє видалити newElement з документа.
secondDiv.remove();

// innerHTML
// Визначення: властивість innerHTML встановлює або повертає вміст HTML в елементі.
console.log(newElement.innerHTML);
a.innerHTML = "<strong>New Text For a link with a wrapper</strong>";
// a.textContent = '<strong>New Text For a link with a wrapper</strong>';
console.log(newElement.innerHTML);
```

5. **DOM і атрибути**
> **ПИТАННЯ**: Назвіть різні атрибути? Що таке атрибути? Як отримати атрибут елемента?

**Результат**:

```js
console.clear();

// Стандартні атрибути та властивості
let linkId = a.id;
console.log(linkId);
let classNameOfH1 = h1.className;
console.log(classNameOfH1);

// Зміна класів
h1.classList.add("some-cool-class");
console.log(h1.classList.contains("some-cool-class"));
h1.classList.remove("some");
h1.classList.toggle("active");
h1.classList.toggle("active");

console.log(h1.classList.contains("active"));

// Атрибути читання та запису
let attribute = "someNonStandardAttribute";
h1.setAttribute(attribute, "New Non Standard Value");
// Отримати атрибут: отримує значення вказаного атрибута.
console.log(h1.getAttribute(attribute));
// Має атрибут: перевіряє, чи має елемент вказаний атрибут.
console.log(h1.hasAttribute(attribute));

// Дані-атрибути
let h1DataName = h1.dataset.name;
let h1DataOneMore = h1.dataset.oneMore;

console.log(h1DataName, h1DataOneMore);
```

6. **Опис вимог до практичного завдання.** Подробиці дивіться в [DISCLAIMER.md](../DISCLAIMER.md).