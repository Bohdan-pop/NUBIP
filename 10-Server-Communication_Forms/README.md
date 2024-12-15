# Веб-розробка - серверне спілкування та форми

Цей документ є планом сесії запитань і відповідей за темами навчального курсу:
Функції (https://university.epam.com/learning-piece/sharing?rootId=6456574&itemId=6456628)

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

1. Який метод використовується для надсилання HTTP-запиту та отримання відповіді в сучасному JavaScript?

- JSON.stringify
- ✅: Fetch
- HTTP.parse

2. Що робить JSON.stringify?

- ✅: конвертує об’єкт у JSON
- Розбирає дані JSON
- Отримує JSON із сервера

3. Яка технологія забезпечує двонаправлений зв’язок у реальному часі між клієнтом і сервером?

- XMLHttpRequest
- Fetch API
- ✅: WebSockets

4. Який метод використовується для програмного надсилання форми в JavaScript?

- Form.send()
- ✅: Form.submit()
- Form.post()

5. Як отримати доступ до значення елемента форми за допомогою JavaScript?

- Form.getElementValue()
- ✅: FormElement.value
- FormElement.getValue()

6. Який метод використовується для очищення даних форми?
- ✅: Form.reset()
- Form.clear()
- Form.empty()

## 2. Теоретичні теми

1. **GET, POST, PUT, DELETE**

> **ПИТАННЯ**: Як створити запит GET? Як розібрати відповідь? Як обробляти помилки?

**Результат:**
CODEPEN: https://codepen.io/homerous/pen/bGzvMoM

```js
console.clear();

// Виклик `fetch()`, передаючи URL-адресу.
// ОТРИМАТИ отримати всі справи
fetch("https://jsonplaceholder.typicode.com/todos")
 // fetch() повертає обіцянку. Коли ми отримали відповідь від сервера,
 // обробник `then()` обіцянки викликається з відповіддю.
  .then((response) => {
 // Наш обробник видає помилку, якщо запит не виконано.
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
 // В іншому випадку (якщо відповідь успішна), наш обробник отримує відповідь
 // як текст, викликаючи response.text(), і негайно повертає обіцянку
 // повертається `response.text()`.
    return response.text();
 })
 // Коли response.text() виконано успішно, обробник `then()` викликається з
 // text, і ми копіюємо його в поле `poemDisplay`.
  .then((text) => {
    console.log("Method: GET, endpoint: /todos, responce: ", text);
  })
 // Виявляти будь-які помилки, які можуть статися, і виводити повідомлення
 // у полі `poemDisplay`.
  .catch((error) => {
    console.log(`Error: ${error}`);
  });

// POST додає до надісланого об’єкта випадковий ідентифікатор
fetch("https://jsonplaceholder.typicode.com/todos", {
  method: "POST",
  body: JSON.stringify({
    userId: 1,
    title: "clean room",
    completed: false,
  }),
  headers: {
    "Content-type": "application/json; charset=UTF-8",
  },
})
  .then((response) => response.json())
  .then((json) =>
    console.log("Method: POST, endpoint: /todos, responce: ", json)
  );

// PUT додає до ресурсу з id = 5, щоб змінити назву завдання
fetch("https://jsonplaceholder.typicode.com/todos/5", {
  method: "PUT",
  body: JSON.stringify({
    userId: 1,
    id: 5,
    title: "hello task",
    completed: false,
  }),
  headers: {
    "Content-type": "application/json; charset=UTF-8",
  },
})
  .then((response) => response.json())
  .then((json) =>
    console.log("Method: PUT, endpoint: /todos/5, responce: ", json)
  );

// DELETE видалити завдання з id = 1
fetch("https://jsonplaceholder.typicode.com/todos/1", {
  method: "DELETE",
});
```

2. **WebSocket**

> **ПИТАННЯ**: що таке WebSocket? Як створити підключення WebSocket? Як відправляти та отримувати повідомлення?

**Результат**:
CODEPEN: https://codepen.io/homerous/pen/gOqedZv

```html
<div>Ethereum : <span id="stock-price">----</span></div>
```

```js
console.clear();

const ws = new WebSocket("wss://stream.binance.com:9443/ws/etheur@trade");
const stockPriceElement = document.getElementById("stock-price");
let lastPrice = null;

ws.onmessage = (event) => {
  const stockObject = JSON.parse(event.data);
  const price = parseFloat(stockObject.p).toFixed(2);
  stockPriceElement.innerText = price;
  stockPriceElement.style.color =
    !lastPrice || lastPrice === price
      ? "black"
      : price > lastPrice
        ? "green"
        : "red";
  lastPrice = price;
};
```

3. **XMLHttpRequest**
> **ПИТАННЯ** Що таке XMLHttpRequest? Як створити XMLHttpRequest? Як відправляти та отримувати повідомлення?

**Результат**:
CODEPEN: https://codepen.io/homerous/pen/mdvxGdr

**Result**:
CODEPEN: https://codepen.io/homerous/pen/mdvxGdr

```html
<div class="container">
  <h1>Welcome To Random Dog Pictures</h1>
  <img
    id="photo"
    src="https://images.dog.ceo/breeds/segugio-italian/n02090722_001.jpg"
    alt=""
  />
  <button id="button">Get Random Dog!</button>
</div>
```

```css
img {
  height: 200px;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

button {
  margin: 20px;
}
```

```js
console.clear();

var img = document.querySelector("#photo");
var button = document.querySelector("#button");
button.addEventListener("click", () => {
  let xhr = new XMLHttpRequest();

  xhr.onreadystatechange = function () {
    if (xhr.readyState == 4 && xhr.status == 200) {
      let url = JSON.parse(xhr.responseText).message;
      img.src = url;
    }
  };
  xhr.open("GET", "https://dog.ceo/api/breeds/image/random");
  xhr.send();
});
```

4. **Форма**
> **ПИТАННЯ** Що таке форма? Як створити форму? Як надіслати дані форми під час надсилання?

**Результат**:
CODEPEN: https://codepen.io/homerous/pen/vYbRzVJ

```html
<div class="container">
  <div class="header">
    <h2>Create Account</h2>
  </div>
  <form action="" class="form" id="form">
    <div class="form-control">
      <label>Username</label>
      <input type="text" placeholder="Your username" id="username" />
      <i class="fas fa-check-circle"></i>
      <i class="fas fa-exclamation-circle"></i>
      <small>Error message</small>
    </div>
    <div class="form-control">
      <label>Email</label>
      <input type="email" placeholder="Your Email" id="email" />
      <i class="fas fa-check-circle"></i>
      <i class="fas fa-exclamation-circle"></i>
      <small>Error message</small>
    </div>
    <div class="form-control">
      <label>Password</label>
      <input type="password" placeholder="Your password" id="password" />
      <i class="fas fa-check-circle"></i>
      <i class="fas fa-exclamation-circle"></i>
      <i class="far fa-eye" id="show" onclick="togglePassword()"></i>
      <i class="far fa-eye-slash" id="hide" onclick="togglePassword()"></i>
      <small>Error message</small>
    </div>
    <div class="form-control">
      <label>Confirm</label>
      <input type="password" placeholder="Your password again" id="password2" />
      <i class="fas fa-check-circle"></i>
      <i class="fas fa-exclamation-circle"></i>
      <i class="far fa-eye" id="show2" onclick="toggleConfirm()"></i>
      <i class="far fa-eye-slash" id="hide2" onclick="toggleConfirm()"></i>
      <small>Error message</small>
    </div>

    <button>Submit</button>
  </form>
</div>
```

```css
@import url("https://fonts.googleapis.com/css?family=Raleway&display=swap");

* {
  box-sizing: border-box;
}

body {
  font-family: "Raleway", sans-serif;
  background: #9b59b6;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  margin: 0;
}

.container {
  background: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
  overflow: hidden;
  width: 400px;
  max-width: 100%;
}

.header {
  background: #f7f7f7;
  border-bottom: 1px solid #f0f0f0;
  padding: 20px 40px;
}

.header h2 {
  margin: 0;
}

.form {
  padding: 30px 20px;
}

.form-control {
  margin-bottom: 10px;
  padding-bottom: 20px;
  position: relative;
}

.form-control label {
  display: inline-block;
  margin-bottom: 5px;
}

.form-control input {
  border: 2px solid #f0f0f0;
  border-radius: 2px;
  display: block;
  font-family: inherit;
  font-size: 14px;
  padding: 10px;
  width: 100%;
}

.form-control.success input {
  border-color: #2ecc71;
}

.form-control.error input {
  border-color: #e74c3c;
}

.form-control i {
  visibility: hidden;
  position: absolute;
  top: 36px;
  right: 10px;
}

.form-control i.fa-eye {
  visibility: visible;
  cursor: pointer;
}

.form-control i.fa-eye-slash {
  visibility: hidden;
  cursor: pointer;
}

.form-control.success i.fa-check-circle {
  visibility: visible;
  color: #2ecc71;
  top: 36px;
  right: 30px;
}

.form-control.error i.fa-exclamation-circle {
  visibility: visible;
  color: #e74c3c;
  top: 36px;
  right: 30px;
}

.form-control small {
  visibility: hidden;
  position: absolute;
  bottom: 0;
  left: 0;
}

.form-control.error small {
  visibility: visible;
  color: #e74c3c;
}

.form button {
  background: #8e44ad;
  border: 2px solid #8e44ad;
  border-radius: 2px;
  color: #fff;
  display: block;
  width: 100%;
  padding: 10px;
  font-size: 16px;
  font-family: inherit;
}
```

```js
console.clear();

const form = document.getElementById("form");

const username = document.getElementById("username");
const email = document.getElementById("email");
const password = document.getElementById("password");
const password2 = document.getElementById("password2");

form.addEventListener("submit", (e) => {
  e.preventDefault();

  checkInputs();
});

const checkInputs = () => {
  // Get values from the inputs
  const usernameValue = username.value.trim();
  const emailValue = email.value.trim();
  const passwordValue = password.value.trim();
  const password2Value = password2.value.trim();

  if (!usernameValue) {
    //Show error
    //Add error class
    setErrorFor(username, "Username cannot be blank");
  } else {
    //Add succes class
    setSuccessFor(username);
  }

  if (!emailValue) {
    //Show error
    //Add error class
    setErrorFor(email, "Email cannot be blank");
  } else if (!isEmail(emailValue)) {
    //Show error
    //Add error class
    setErrorFor(email, "Email is not valid");
  } else {
    //Add succes class
    setSuccessFor(email);
  }

  const re = /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{6,20}$/;
  if (!passwordValue) {
    //Show error
    //Add error class
    setErrorFor(password, "Password cannot be blank");
  } else if (passwordValue.length < 8) {
    //Add succes class
    setErrorFor(password, "Password to short");
  } else if (!passwordValue.match(re)) {
    //Add succes class
    setErrorFor(password, "it have to contains a upper, lower and a number");
  } else {
    //Add succes class
    setSuccessFor(password);
  }

  if (!password2Value) {
    //Show error
    //Add error class
    setErrorFor(password2, "write again your password");
  } else if (passwordValue !== password2Value) {
    //Add succes class
    setErrorFor(password2, "does not match");
  } else {
    //Add succes class
    setSuccessFor(password2);
  }

  //HomeWork mostrar un mensaje de exito al hacer click y todo este correcto
};

const setErrorFor = (input, message) => {
  const formControl = input.parentElement; //this is the .form-control
  const small = formControl.querySelector("small");

  //add error message inside small
  small.innerText = message;

  //add error class
  formControl.className = "form-control error";
};

const setSuccessFor = (input) => {
  const formControl = input.parentElement; //this is the .form-control

  //add success class
  formControl.className = "form-control success";
};

const isEmail = (email) => {
  //this checks if the email is valid
  return /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(
    email
  );
};

const togglePassword = () => {
  const psw = document.getElementById("password");
  const show = document.getElementById("show");
  const hide = document.getElementById("hide");

  if (psw.type === "password") {
    psw.type = "text";
    show.style.visibility = "hidden";
    hide.style.visibility = "visible";
  } else {
    psw.type = "password";
    show.style.visibility = "visible";
    hide.style.visibility = "hidden";
  }
};

const toggleConfirm = () => {
  const confirm = document.getElementById("password2");

  const show2 = document.getElementById("show2");
  const hide2 = document.getElementById("hide2");

  if (confirm.type === "password") {
    confirm.type = "text";
    show2.style.visibility = "hidden";
    hide2.style.visibility = "visible";
  } else {
    confirm.type = "password";
    show2.style.visibility = "visible";
    hide2.style.visibility = "hidden";
  }
};
```

5. **Опис вимог до практичного завдання.** Подробиці дивіться в [DISCLAIMER.md](../DISCLAIMER.md).