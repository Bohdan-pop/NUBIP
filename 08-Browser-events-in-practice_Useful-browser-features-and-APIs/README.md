# Веб-розробка - події браузера на практиці та корисні функції браузера та API

https://uk.javascript.info/browser-environment
https://uk.javascript.info/onload-ondomcontentloaded
https://uk.javascript.info/url
https://uk.javascript.info/default-browser-action
https://uk.javascript.info/pointer-events
https://uk.javascript.info/introduction-browser-events
https://uk.javascript.info/dispatch-events

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

- ✅: правильна відповідь
- [необов’язково]: необов’язкова тема, запитання або приклад коду. Це залежить від відповідей учнів. Якщо вони вже це знають, ви можете пропустити це.

**Питання:**

1. Яка подія браузера запускається, коли вказівник миші вводить елемент?
   - Input
   - ✅ Mouseover
   - Change

2. Яка подія відбувається при натисканні клавіші Enter у полі введення тексту?

   - Submit
   - ✅ Keyup
   - Change

3. Чим подія Load відрізняється від події DOMContentLoaded?

- ✅  Load, очікування для всіх ресурсів; DOMContentLoaded, коли HTML повністю проаналізовано
- DOMContentLoaded очікує на всі ресурси; Load, коли HTML повністю проаналізовано
  – Це та сама подія

4. Який механізм збереження даних браузера використовується для зберігання даних лише до моменту закриття браузера?

   - LocalStorage
   - Cookies
   - ✅ SessionStorage

5. Який API забезпечує можливість переходу вперед і назад в історії браузера?

   - Location API
   - ✅ History API
   - Navigate API
   - 
6. Яке основне використання файлів cookie у веб-розробці?
- Взаємодія через браузер
- Керування стилями CSS
- ✅: Відстеження даних користувачів і сеансів

## 2. Теоретичні теми

1. **Події миші та клавіатури**

> **ПИТАННЯ**: що таке події миші та як їх можна обробляти в JavaScript? Як ви можете прослуховувати події клавіатури в браузері за допомогою JavaScript?

**Результат:**

```html
<div class="hover" id="hover">Hover over me!</div>
```

```css
.hover {
  padding: 50px;
  margin-bottom: 10px;
  width: 200px;
  text-align: center;
  border: 2px solid black;
}
```

```js
console.clear();

const hover = document.getElementById("hover");

// Mouse Events
hover.addEventListener("mouseover", () => {
  console.log("Mouse over the div");
});

hover.addEventListener("mouseout", () => {
  console.log("Mouse left the div");
});

hover.addEventListener("mouseenter", () => {
  console.log("Mouse entered the div");
});

hover.addEventListener("mouseleave", () => {
  console.log("Mouse left the div (alternative)");
});

// Keyboard Events
document.addEventListener("keydown", (event) => {
  console.log("Key pressed: " + event.key);
});
```

2. **Подія введення**

> **ПИТАННЯ**: Як перевірити вхідні дані? Як обробляти події введення?

**Результат**:

```html
<input type="text" id="phoneInput" placeholder="Enter phone number" />
<button id="submitButton">Submit</button>
<div class="phone-form__valid-mark hidden">✅ Valid phone number</div>
```

```css
.hidden {
  display: none;
}
```

```js
console.clear();

const phoneInput = document.getElementById("phoneInput");
const submitButton = document.getElementById("submitButton");
const validMark = document.querySelector(".phone-form__valid-mark");

// Phone Validation
phoneInput.addEventListener("input", () => {
 const phonePattern = /^\d{10}$/; // Простий шаблон для 10-значного номера телефону
 const phoneNumber = phoneInput.value;

  if (phonePattern.test(phoneNumber)) {
    validMark.classList.remove("hidden");
    console.log("Valid phone number: " + phoneNumber);
  } else {
    validMark.classList.add("hidden");
    console.log("Invalid phone number: " + phoneNumber);
  }
});

submitButton.addEventListener("click", () => {
  const phoneNumber = phoneInput.value;
  if (validMark.classList.contains("hidden")) {
    console.log("Please enter a valid phone number first.");
  } else {
    console.log("Submitting valid phone number: " + phoneNumber);
  }
});
```


3. **Користувацькі події та події завантаження сторінки**
> **ПИТАННЯ**: що таке користувацькі події, і як їх можна створювати та запускати в JavaScript? Як ви можете прослухати події завантаження в браузері за допомогою JavaScript?

**Результат**:

```html
<button id="customDiv">Custom Event Example</button>
<button id="triggerCustomEvent">Trigger Custom Event</button>
```

```js
console.clear();

const customDiv = document.getElementById("customDiv");
const triggerCustomEventButton = document.getElementById("triggerCustomEvent");

// Custom Event
// Це дозволяє вам визначити свій власний тип події та обробляти його за допомогою слухачів подій.
const customEvent = new Event("myCustomEvent");

customDiv.addEventListener("myCustomEvent", () => {
   console.log("Custom event triggered");
});


// Коли кнопка натиснута, вона запускає настроювану подію в елементі customDiv.
triggerCustomEventButton.addEventListener("click", () => {
 customDiv.dispatchEvent(customEvent);
});

// Події завантаження сторінки
// Подія DOMContentLoaded запускається, коли початковий HTML-документ повністю завантажено та проаналізовано.
// Це корисно для запуску коду JavaScript після того, як структура документа стане доступною.
window.addEventListener("DOMContentLoaded", () => {
   console.log("DOMContentLoaded event fired");
});
// Подія завантаження запускається, коли всі ресурси (зображення, стилі, сценарії тощо) завантажено.
// Це корисно для виконання коду після того, як усі ресурси сторінки готові.
window.addEventListener("load", () => {
   console.log("Load event fired");
});
```

4. **URL браузера**
> **ПИТАННЯ**: як ви можете отримати доступ до URL-адреси веб-сторінки та керувати нею за допомогою API розташування в JavaScript?

**Результат**:

```js
console.clear();

const currentURL = window.location.href;
const host = window.location.host;
const search = window.location.search; // query params

console.log("Current URL: " + currentURL);
console.log("Host: " + host);
console.log("Search: " + search);

// Вилучення параметрів запиту як об'єкта
const urlParams = new URLSearchParams(window.location.search);
const queryParams = {};

for (const [key, value] of urlParams.entries()) {
   queryParams[key] = value;
}

console.log("Query Parameters:", queryParams);
```

5. ** Пам’ять браузера **
> **ПИТАННЯ**: поясніть мету зберігання браузера та як зберігати й отримувати дані за допомогою нього?

**Результат:**

```html
<button id="saveData">Save Data to Storage</button>
<button id="retrieveData">Retrieve Data from Storage</button>
```

```js
console.clear();

const saveDataButton = document.getElementById("saveData");
const retrieveDataButton = document.getElementById("retrieveData");

saveDataButton.addEventListener("click", () => {
  sessionStorage.setItem(
    "user-session",
    JSON.stringify({ name: "John Doe", age: 19, source: "sessionStorage" })
  );
  localStorage.setItem(
    "user-local",
    JSON.stringify({ name: "John Wick", age: 42, source: "localStorage" })
  );
  console.log("Data saved!");
});

retrieveDataButton.addEventListener("click", () => {
  const storedSessionData = sessionStorage.getItem("user-session");
  const storedLocalData = localStorage.getItem("user-local");

  if (storedLocalData) {
    const userSession = JSON.parse(storedSessionData);
    console.log("Data retrieved from session storage:", userSession);

    const userLocal = JSON.parse(storedLocalData);
    console.log("Data retrieved from local storage:", userLocal);
  } else {
    console.log("No data found in session storage");
  }
});
```


6. **Cookie**
> **ПИТАННЯ**: поясніть концепцію файлів cookie у веб-розробці та як можна встановити та отримати файли cookie за допомогою JavaScript?

**Результат:**

```html
<button id="setCookie">Set Cookie</button>
<button id="getCookie">Get Cookie</button>
```

```js
console.clear();

// Cookies
document.getElementById("setCookie").addEventListener("click", () => {
  document.cookie =
    "username=JohnDoe; expires=Fri, 31 Dec 2023 23:59:59 GMT; path=/";
  console.log("Cookie set!");
});

document.getElementById("getCookie").addEventListener("click", () => {
  const username = document.cookie.split("=")[1];
  console.log("Username: " + username);
});
```


7. **Опис вимог до практичного завдання.** Подробиці дивіться в [DISCLAIMER.md](../DISCLAIMER.md).