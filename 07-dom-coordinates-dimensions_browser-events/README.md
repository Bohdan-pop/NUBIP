# Веб-розробка - Координати та розміри елементів DOM і основи подій браузера

https://uk.javascript.info/searching-elements-dom
https://uk.javascript.info/events
https://uk.javascript.info/bubbling-and-capturing
https://uk.javascript.info/coordinates
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

1. Яка різниця між `offsetWidth` і `clientWidth`?

- `offsetWidth` включає ширину смуги прокрутки.
- `offsetWidth` також включає ширину рамки.
- ✅: Все вищезазначене.

2. Це та сама дія: `elem.classList.add("active")` і `elem.className = "active"`?

- так.
- Ні, приклад `className` видає помилку.
- ✅: Ні, коли ви призначаєте `elem.className`, це стирає всі існуючі назви класів.

3. Чи існує подія для відстеження прокручування сторінок?

- ✅: Так, він називається "scroll"
- Так, це називається "onscroll"
  – Ні, такої події немає, але вона буде в майбутньому.

4. Як додати прослуховувач (listener) подій для події "клацання" за допомогою атрибута?

   - ✅: <button onclick="console.log('click');">Click</button>
   - <button onclick="console.log">Click</button>
   - <button onclick="function() { console.log('click') }">Click</button>

5. Як називається метод додавання кількох обробників подій для одного елемента й тієї самої події?

- ✅: elem.addEventListener
- elem.addListener
- elem.listener
- elem.listen

6. Як дізнатися, що була натиснута кнопка CTRL(CMD), коли сталася подія «click»?

- Ви не можете отримати цю інформацію.
- ✅: Ви отримуєте його з об’єкта події (event object).
- Ви отримуєте його, викликаючи метод `document.isCtrlPressed`

## 2. Теоретичні теми

### Приклади координат і розмірів елементів DOM

1. **Розміри DOM**
> **ПИТАННЯ**: Чи можете ви навести приклад того, коли нам потрібно працювати з розмірами прокручування чи елемента? З точки зору користувача.

**Результат:**

```html
<h1>Some cool website</h1>

<button class="button_reveal button">Show Page Dimensions</button>

<nav class="menu">
   <button class="Option1">Option1</button>
   <button class="Option1">Option1</button>
   <button class="Option1">Option1</button>
   <button class="Option1">Option1</button>
   <button class="Option1">Option1</button>
   <button class="Option1">Option1</button>
</nav>

<div class="controls">
   <button class="button button_show-scroll">Show scroll</button>
   <button class="button button_back">←</button>
   <button class="button button_forward">→</button>
</div>

<button class="button button_scroll-top">⬆</button>

<p>
   Lorem ipsum dolor sit amet consectetur adipisicing elit. Doloremque neque
   facere ea iste cupiditate explicabo nam nobis? Laborum dolorum reiciendis
   voluptates quia odio, autem, sit quisquam harum quis consectetur omnis.
   Aperiam, ratione eveniet obcaecati laboriosam, debitis placeat, recusandae
   temporibus dolorum dolores excepturi eum? Deleniti quam culpa ipsum amet
   facilis neque, distinctio ut ex eligendi at aut corporis autem vero nam. Aut
   ipsum perferendis sed sunt mollitia et neque deserunt rerum quas tenetur
   dolores laboriosam iusto, commodi magni praesentium facere nisi repellat
   fugiat assumenda, officiis aliquid enim. Ea consequuntur mollitia laboriosam.
   Maxime aspernatur qui non ipsam eos commodi reiciendis exercitationem alias,
   quas, officia porro ab nostrum corporis deserunt id? Iusto omnis autem quos.
   Architecto illo possimus voluptatibus nulla neque quas hic. Placeat inventore
   officiis impedit dolor ipsam, similique odit alias culpa eligendi nobis fuga
   deleniti eveniet molestias odio, vel reiciendis, enim libero laudantium
   consectetur voluptatibus expedita illum? Eaque, eveniet. Facilis, laudantium!
</p>
```

```css
p {
   border: 2px solid #bada55;
}

.button {
   padding: 5px;
   font-size: 14px;
}

.button_reveal {
   position: fixed;
   right: 20px;
   top: 20px;
}

.button_scroll-top {
   position: fixed;
   bottom: 20px;
   right: 20px;
}

.menu {
   width: 200px;
   padding: 10px;
   border: 2px solid #bada55;
   overflow: auto;
   white-space: nowrap;
}

.controls {
   padding-top: 10px;
}
```

```js
console.clear();

let menu = document.querySelector(".menu");
let revealButton = document.querySelector(".button_reveal");
let buttonShowScroll = document.querySelector(".button_show-scroll");
let buttonForward = document.querySelector(".button_forward");
let buttonBack = document.querySelector(".button_back");
let buttonScrollTop = document.querySelector(".button_scroll-top");

// Розмір елемента та прокрутка
buttonShowScroll.onclick = function () {
   console.log("offsetHeight: ", menu.offsetHeight);
   console.log("offsetWidth: ", menu.offsetWidth);
 // Вони дорівнюють нулю, коли елемент приховано або поза сторінкою

 // Ці властивості забезпечують розмір області всередині меж елемента.
   console.log("clientWidth: ", menu.clientWidth);
   console.log("clientHeight: ", menu.clientHeight);

   console.log("clientTop: ", menu.clientTop);
   console.log("clientLeft: ", menu.clientLeft);

 // Параметри прокрутки
 // Властивості scrollLeft/scrollTop — це ширина/висота прихованої, прокрученої частини елемента.
   console.log("scrollLeft: ", menu.scrollLeft);
   console.log("scrollTop: ", menu.scrollTop);
   console.log("scrollWidth: ", menu.scrollWidth);
   console.log("scrollHeight: ", menu.scrollWidth);
};


// Розмір сторінки та прокрутка
revealButton.onclick = showCoordinates;
function showCoordinates() {
 // Розміри вікна перегляду
   let clientWidth = document.documentElement.clientWidth;
   let clientHeight = document.documentElement.clientHeight;

   console.log("clientWidth: ", clientWidth, "clientHeight: ", clientHeight);

 // Поточний Scroll
 let pageYOffset = window.pageYOffset;
 let pageXOffset = window.pageXOffset;

 // Також можна використовувати ScrollTop і scrollLeft
   console.log("pageYOffset: ", pageYOffset, document.documentElement.scrollTop);
   console.log(
           "pageXOffset: ",
           pageXOffset,
           document.documentElement.scrollLeft
   );
}

// Методи прокручування
buttonForward.onclick = function () {
   menu.scrollBy(10, 0);
};

buttonBack.onclick = function () {
   menu.scrollBy({ top: 0, left: -10, behavior: "smooth" }); // smooth, instant, auto
};

// Menu scrolled!
menu.onscroll = function () {
   console.log("Menu scrolled!", menu.scrollLeft);
};


// Прокрутити сторінку вгору
buttonScrollTop.onclick = function () {
   // document.documentElement.scrollTo(0, 0);
   document.documentElement.scrollTo({ top: 0, left: 0, behavior: "smooth" });
};
```

2. **Координати елемента**

> **ПИТАННЯ**: Як отримати координати елемента?

**Опис завдання:**

- Створіть функцію `createMessage`, яка створює елемент повідомлення `<div>` і розміщує його в елементі з іменем класу `selected-user`.
- Елемент повідомлення має розташовуватися точно і на нього не повинно впливати прокручування сторінки.
- Ми починаємо представляти це завдання з HTML і CSS і додаємо код крок за кроком.

**Результат**:

```html
<ul>
   <li>User 1</li>
   <li>User 2</li>
   <li>User 3</li>
   <li>User 4</li>
   <li class="selected-user">User 5</li>
   <li>User 6</li>
   <li>User 7</li>
   <li>User 8</li>
   <li>User 9</li>
</ul>

<p>
   Lorem ipsum dolor sit amet consectetur adipisicing elit. Totam, maiores fugiat
   assumenda quae quas beatae suscipit labore repellat est ab accusantium laborum
   sequi maxime officia nobis ipsum ut dignissimos necessitatibus! At facere, et
   porro quisquam quia nemo hic amet, corrupti tenetur est voluptatum iste
   exercitationem sint doloribus reiciendis neque a quo illum vitae ab obcaecati.
   Quibusdam repellendus architecto sequi recusandae. Totam deleniti dolor
   laboriosam laudantium aut sapiente repellendus in, reiciendis quis ipsum
   molestias quae, iure maiores aperiam dignissimos excepturi voluptatem deserunt
   sunt maxime blanditiis explicabo omnis culpa? Cumque, corporis magni. Sunt
   omnis error eum maiores ullam porro vel adipisci impedit aliquid ipsum culpa
   corrupti distinctio voluptatibus expedita, reprehenderit obcaecati quam!
   Accusamus quam qui error molestias incidunt exercitationem eligendi
   perspiciatis aspernatur. Quae provident adipisci laboriosam! Assumenda
   dignissimos laboriosam modi officiis. Tempora rem nam, deserunt expedita
   voluptas inventore perspiciatis consectetur, corrupti assumenda voluptatum
   illum dolorum quo voluptates explicabo ratione repudiandae dolor eveniet. Esse
   non harum dolor dolorem aperiam eveniet aut ad, facere asperiores assumenda
   sint temporibus tempore nesciunt nisi quaerat? Nam veniam voluptas odit
   deleniti molestias. Optio repellat eaque voluptate accusantium aliquid!
   Consequatur id ut rerum iusto nostrum sapiente cupiditate eveniet magnam. Qui
   blanditiis consequuntur recusandae voluptas, molestiae iste numquam distinctio
   repellat optio ea reprehenderit repellendus aspernatur ducimus eos. Id, omnis
   ex! Saepe commodi fuga illo et repudiandae rem soluta aperiam ipsum atque
   natus minima voluptas aliquid neque ex, itaque molestiae. Consectetur id
   placeat fugiat aut ullam, laborum voluptatum exercitationem excepturi odio.
   Omnis harum corrupti deleniti rem quasi adipisci perferendis fugit, itaque
   blanditiis deserunt commodi debitis dignissimos nemo dolorum ad perspiciatis
   laboriosam atque numquam enim repellat, facilis cum quis autem. Autem, sit.
</p>

<button style="position: fixed; top: 50px; right: 20px;" class="create-message">
   Create Message
</button>
```

```css
li {
   width: 200px;
   margin-top: 20px;
   padding: 5px;
   border: 2px solid #bada55;
}

.selected-user {
   font-weight: bold;
   border-color: blue;
}
```

```js
console.clear();

let selectedUser = document.querySelector(".selected-user");

let clientRect = selectedUser.getBoundingClientRect();

console.log(clientRect);

function createMessage() {
   let message = document.createElement("div");
   message.style.cssText = "position:absolute; color: red;";

   message.innerHTML = "Hello, world!";

   let clientRect = selectedUser.getBoundingClientRect();

   message.style.left = `${clientRect.left + pageXOffset}px`;
   message.style.top = `${clientRect.bottom + pageYOffset}px`;

   document.body.append(message);
}

document
        .querySelector(".create-message")
        .addEventListener("click", createMessage);
```

### Основні приклади подій браузера

3. **Додати обробник подій**

```html
<button>I am button, button, button</button>
```

```js
console.clear();

let button = document.querySelector("button");

// Ми не можемо додати два або більше окремих обробників подій за допомогою властивостей
button.onclick = highLight;
button.onclick = send;

function highLight() {
   console.log("Highlight!");
}

function send() {
   console.log("Send!");
}

// Однак ми можемо зробити це за допомогою методу addEventListener
button.addEventListener("click", highLight);
button.addEventListener("click", send);

button.removeEventListener("click", highLight);

// Запитання до студентів: чи видаляє наведений нижче код обробник подій?
button.addEventListener("click", () => console.log("Any action!"));
button.removeEventListener("click", () => console.log("Any action!"));
// Відповідь: ні, це не так. Ви повинні надати ту саму функцію, коли видаляєте обробник подій.

// Параметри параметрів addEventListener
function touch(event) {
   console.log("Touch! But Only Once");
}

// Коли ви вказуєте властивість "one", обробник події працює лише один раз
button.addEventListener("click", touch, { once: true });

// Об'єкт події
function check(event) {
   console.log(
           "Event Object: ",
           event.type,
           event.target,
           event.clientX,
           event.clientY
   );
}

button.addEventListener("click", check);

// Запобігання замовчуванню
// Для деяких дій користувача браузер має поведінку за замовчуванням
// Але ми можемо цьому запобігти
let jsLink = document.querySelector(".js-link");

jsLink.onclick = function (event) {
   event.preventDefault();

   console.log("We handle a link click here!");
};
```

4. **Bubbling, вспливання подій**

```html
<style>
   body * {
      margin: 10px;
      border: 1px solid blue;
   }
</style>

<form>
   FORM
   <div>
      DIV
      <p>P</p>
   </div>
</form>
```

```js
console.clear();

// Майже всі події браузера висвітлюються. Давайте подивимося, як це працює.
let form = document.querySelector("form");
let div = document.querySelector("div");
let p = document.querySelector("p");

form.addEventListener("click", function (event) {
   console.log("form");
   // console.log('form', event.target.tagName, event.currentTarget.tagName, this.tagName);
});

div.addEventListener("click", function (event) {
   console.log("div");
});

p.addEventListener("click", function (event) {
   console.log("p");
 // Щоб зупинити витікання події, ви можете викликати метод stopPropagation для об’єкта події
 // Якщо розкоментувати цей код, подія припиняє випливати
 // event.stopPropagation();
});
```

5. **[НЕОБОВ’ЯЗКОВО] Додати кнопку «Закрити» до текстових карток**

**Опис завдання:**

- Додайте до кожного елемента з іменем класу `pane` кнопку закриття: `<button class="remove-button">[x]</button>`
  — Додано слухач подій для видалення елемента з класом `pane` після того, як користувач натисне цю кнопку.
- Ми починаємо представляти це завдання з HTML і CSS і додаємо код крок за кроком.

```html
<div class="panes">
  <div class="pane">
    <h3>Horse</h3>
    <p>
      The domestic horse is an animal of the family of artiodactyls, a
      domesticated and the only surviving subspecies of a wild horse that is
      extinct in the wild, except a small population of the Przewalski's horse.
    </p>
  </div>
  <div class="pane">
    <h3>Donkey</h3>
    <p>
      Domestic donkey (lat. Equus asinus asinus), or donkey, is a domesticated
      subspecies of the wild donkey (Equus asinus), which played an important
      historical role in the development of the economy and human culture and is
      still widely used in the economy of many developing countries.
    </p>
  </div>
  <div class="pane">
    <h3>Cat</h3>
    <p>
      A cat, or domestic cat (lat. Felis silvestris catus), is a pet, one of the
      most popular (along with a dog) “companion animals”. As a solitary hunter
      of rodents and other small animals, the cat is a social animal, using a
      wide range of vocal cues to communicate.
    </p>
  </div>
</div>
```

```css
body {
  margin: 10px auto;
  width: 470px;
}

h3 {
  margin: 0;
  padding-bottom: 0.3em;
  font-size: 1.1em;
}

p {
  margin: 0;
  padding: 0 0 0.5em;
}

.pane {
  position: relative;
  background: #edf5e1;
  padding: 10px 20px 10px;
  border-top: solid 2px #c4df9b;
}

.remove-button {
  position: absolute;
  top: 5px;
  right: 5px;
  font-size: 110%;
  color: darkred;
  right: 10px;
  width: 24px;
  height: 24px;
  border: none;
  background: transparent;
  cursor: pointer;
}
```

```js
let button = '<button class="remove-button">[x]</button>';

let panes = document.querySelectorAll(".pane");
console.log(panes);

for (let pane of panes) {
  pane.insertAdjacentHTML("afterbegin", button);
  let removeButton = pane.querySelector(".remove-button");

  removeButton.addEventListener("click", function () {
    pane.remove();
  });
}
```


6. **Опис вимог до практичного завдання.** Подробиці дивіться в [DISCLAIMER.md](../DISCLAIMER.md).