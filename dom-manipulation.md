# DOM манипуляции 🏗️

## 🎦 Что такое DOM?

Представь DOM как **чертеж дома в браузере**:

🏠 **HTML документ** = реальный дом  
📋 **DOM** = подробный чертеж дома  
👷 **JavaScript** = строитель, который меняет дом по чертежу

```javascript
// DOM = Document Object Model (Объектная модель документа)
// Это JavaScript представление HTML-структуры страницы
```

## 🔍 Поиск элементов

### 🎯 document.querySelector() - самый мощный

```javascript
// Поиск по ID
const title = document.querySelector("#main-title");

// Поиск по классу
const button = document.querySelector(".btn-primary");

// Поиск по тегу
const paragraph = document.querySelector("p");

// Поиск по атрибуту
const link = document.querySelector("[href='https://example.com']");

// Сложные селекторы CSS
const element = document.querySelector("div.container > ul.list li.active");
```

### 🎯 document.querySelectorAll() - много элементов

```javascript
// Все кнопки
const allButtons = document.querySelectorAll("button");

// Все elements с классом
const cards = document.querySelectorAll(".card");

// Получаем NodeList (похож на array, но не совсем)
console.log(allButtons.length); // количество элементов

// Обход элементов
allButtons.forEach((button) => {
  button.textContent = "Нажми меня!";
});
```

### 🎯 Старые методы (все еще работают)

```javascript
// Поиск по ID (быстрее querySelector)
const element = document.getElementById("my-id");

// Поиск по имени класса (возвращает HTMLCollection)
const elements = document.getElementsByClassName("my-class");

// Поиск по тегу
const paragraphs = document.getElementsByTagName("p");
```

### 🎯 Относительный поиск

```javascript
const parent = document.querySelector(".parent");

// Найти внутри родителя
const child = parent.querySelector(".child");

// Найти все внутри родителя
const allChildren = parent.querySelectorAll(".child");

// Прямые потомки
const directChildren = parent.children;

// Предок
const ancestor = element.closest(".container");
```

## 🏗️ Создание элементов

### 🎯 document.createElement()

```javascript
// Создаем element
const button = document.createElement("button");

// Настраиваем
button.textContent = "Нажми меня!";
button.className = "btn btn-primary";
button.id = "my-button";

// Атрибуты
button.setAttribute("data-action", "submit");
button.disabled = false;

console.log(button); // <button class="btn btn-primary" id="my-button" data-action="submit">Нажми меня!</button>
```

### 🎯 Создание с HTML

```javascript
// Быстрое создание (безопасно для своего контента)
const card = document.createElement("div");
card.innerHTML = `
    <h3>Заголовок</h3>
    <p>Текст cards</p>
    <button>Кнопка</button>
`;
```

## 📍 Добавление элементов в DOM

### 🎯 appendChild() - oldElement способ

```javascript
const parent = document.querySelector(".container");
const newCard = document.createElement("div");

parent.appendChild(newCard);
```

### 🎯 append() - современный способ

```javascript
const parent = document.querySelector(".container");
const newElement = document.createElement("div");
const text = document.createElement("p");

// Можно добавлять несколько элементов и текста
parent.append(newElement, "Простой text", text);

// prepend - добавить в начало
parent.prepend(newElement);
```

### 🎯 after() и before() - рядом с элементом

```javascript
const element = document.querySelector(".target");
const newElement = document.createElement("div");

element.before(newElement); // Перед элементом
element.after(newElement); // После элемента
```

### 🎯 replaceWith() - замена элемента

```javascript
const oldElement = document.querySelector(".old");
const newElement = document.createElement("div");
newElement.textContent = "Новый element";

oldElement.replaceWith(newElement);
```

## 🗑️ Удаление элементов

### 🎯 remove() - современный способ

```javascript
const element = document.querySelector(".to-remove");
element.remove(); // Элемент удален из DOM
```

### 🎯 removeChild() - oldElement способ

```javascript
const parent = document.querySelector(".parent");
const child = parent.querySelector(".child");
parent.removeChild(child);
```

## 📝 Изменение содержимого

### 🎯 textContent - только text

```javascript
const element = document.querySelector(".message");
element.textContent = "Привет мир!"; // Безопасно от XSS

// Получить text
const text = element.textContent;
```

### 🎯 innerHTML - с HTML (опасно!)

```javascript
const container = document.querySelector(".container");

// ВНИМАНИЕ: небезопасно для пользовательского ввода!
container.innerHTML = "<strong>Жирный text</strong>";

// Опасно для данных от пользователя:
const userInput = "<script>alert('xss')</script>";
container.innerHTML = userInput; // ❌ XSS атака!
```

### 🎯 innerText - как textContent, но с учетом CSS

```javascript
const element = document.querySelector(".text");
element.innerText = "Текст"; // Учитывает display: none и другие CSS правила
```

## 🎨 Работа с атрибутами

### 🎯 getAttribute() / setAttribute()

```javascript
const link = document.querySelector("a");

// Получить атрибут
const href = link.getAttribute("href");

// Установить атрибут
link.setAttribute("href", "https://example.com");
link.setAttribute("target", "_blank");

// Пользовательские атрибуты
link.setAttribute("data-id", "123");
```

### 🎯 Прямые свойства

```javascript
const image = document.querySelector("img");

// Прямые свойства (для стандартных атрибутов)
image.src = "photo.jpg";
image.alt = "Описание фото";
image.width = 300;
image.height = 200;

// Флаги
image.hidden = true; // Скрыть element
```

## 🎨 Работа с классами CSS

### 🎯 className - oldElement способ

```javascript
const element = document.querySelector(".my-element");

element.className = "new-class another-class"; // Полная замена
element.className += " additional-class"; // Добавление
```

### 🎯 classList - современный способ

```javascript
const element = document.querySelector(".my-element");

// Добавить класс
element.classList.add("active");
element.classList.add("btn", "primary"); // Несколько классов

// Удалить класс
element.classList.remove("inactive");

// Переключить класс (добавить если нет, убрать если есть)
element.classList.toggle("visible");

// Проверить наличие класса
const isVisible = element.classList.contains("visible");

// Заменить один класс другим
element.classList.replace("old-class", "new-class");
```

## 🎨 Работа со стилями

### 🎯 Свойство style

```javascript
const element = document.querySelector(".box");

// Установить styles
element.style.color = "red";
element.style.fontSize = "20px";
element.style.backgroundColor = "#f0f0f0";

// Или через setProperty
element.style.setProperty("margin", "10px");
element.style.setProperty("padding", "15px");

// Удалить стиль
element.style.removeProperty("color");

// Получить стиль
const color = element.style.color;
```

### 🎯 getComputedStyle() - вычисленные styles

```javascript
const element = document.querySelector(".box");
const styles = window.getComputedStyle(element);

// Получить вычисленное значение (включая из CSS файлов)
const color = styles.color; // "rgb(255, 0, 0)"
const fontSize = styles.fontSize; // "16px"
const display = styles.display; // "block"
```

## 🎯 Практические примеры

### 🛒 Создание списка дел

```javascript
function createTodoList(container) {
  const title = document.createElement("h2");
  title.textContent = "Список дел";
  container.appendChild(title);

  const list = document.createElement("ul");
  list.className = "todo-list";
  container.appendChild(list);

  const form = document.createElement("form");
  form.innerHTML = `
        <input type="text" placeholder="Введите дело" class="todo-input">
        <button type="submit" class="todo-button">Добавить</button>
    `;
  container.appendChild(form);

  const input = form.querySelector(".todo-input");

  form.addEventListener("submit", (e) => {
    e.preventDefault();

    const text = input.value.trim();
    if (!text) return;

    const element = document.createElement("li");
    element.className = "todo-item";
    element.innerHTML = `
            <span>${text}</span>
            <button class="todo-delete">Удалить</button>
        `;

    list.appendChild(element);
    input.value = "";
    input.focus();

    // Удаление дела
    const deleteButton = element.querySelector(".todo-delete");
    deleteButton.addEventListener("click", () => {
      element.remove();
    });
  });
}

// Использование
const container = document.querySelector("#app");
createTodoList(container);
```

### 🎨 Динамическая gallery изображений

```javascript
function createGallery(container, images) {
  container.className = "gallery";

  images.forEach((src, индекс) => {
    const card = document.createElement("div");
    card.className = "gallery-item";

    const image = document.createElement("img");
    image.src = src;
    image.alt = `Изображение ${индекс + 1}`;
    image.loading = "lazy";

    const caption = document.createElement("div");
    caption.className = "caption";
    caption.textContent = `Фото ${индекс + 1}`;

    card.appendChild(image);
    card.appendChild(caption);
    container.appendChild(card);

    // Клик для увеличения
    card.addEventListener("click", () => {
      createModal(src, `Фото ${индекс + 1}`);
    });
  });
}

function createModal(src, title) {
  // Удаляем существующее modal окно
  const oldModal = document.querySelector(".modal");
  if (oldModal) oldModal.remove();

  const modal = document.createElement("div");
  modal.className = "modal";
  modal.innerHTML = `
        <div class="modal-content">
            <span class="modal-close">&times;</span>
            <img src="${src}" alt="${title}">
            <h3>${title}</h3>
        </div>
    `;

  document.body.appendChild(modal);

  // Закрытие при клике на крестик
  modal.querySelector(".modal-close").addEventListener("click", () => {
    modal.remove();
  });

  // Закрытие при клике на фон
  modal.addEventListener("click", (e) => {
    if (e.target === modal) {
      modal.remove();
    }
  });
}

// Использование
const gallery = ["image1.jpg", "image2.jpg", "image3.jpg"];
const container = document.querySelector("#gallery");
createGallery(container, gallery);
```

### 📊 Создание таблицы из данных

```javascript
function createTable(container, data, headers) {
  const table = document.createElement("table");
  table.className = "data-table";

  // Заголовки
  if (headers) {
    const headerRow = document.createElement("tr");
    headers.forEach((title) => {
      const cell = document.createElement("th");
      cell.textContent = title;
      headerRow.appendChild(cell);
    });
    table.appendChild(headerRow);
  }

  // Данные
  data.forEach((строка_данных) => {
    const row = document.createElement("tr");

    if (Array.isArray(строка_данных)) {
      // Массив значений
      строка_данных.forEach((значение) => {
        const cell = document.createElement("td");
        cell.textContent = значение;
        row.appendChild(cell);
      });
    } else {
      // Объект
      Object.values(строка_данных).forEach((значение) => {
        const cell = document.createElement("td");
        cell.textContent = значение;
        row.appendChild(cell);
      });
    }

    table.appendChild(row);
  });

  container.appendChild(table);
}

// Использование
const data = [
  { имя: "Иван", возраст: 25, город: "Москва" },
  { имя: "Анна", возраст: 30, город: "Санкт-Петербург" },
  { имя: "Борис", возраст: 35, город: "Новосибирск" },
];

const container = document.querySelector("#table-container");
createTable(container, data, ["Имя", "Возраст", "Город"]);
```

### 🎯 Динамическая form

```javascript
function createDynamicForm(fields, container) {
  const form = document.createElement("form");
  form.className = "dynamic-form";

  fields.forEach((поле) => {
    const group = document.createElement("div");
    group.className = "form-group";

    const label = document.createElement("label");
    label.textContent = поле.label + ":";
    label.setAttribute("for", поле.имя);
    group.appendChild(label);

    let input;

    switch (поле.тип) {
      case "textarea":
        input = document.createElement("textarea");
        input.placeholder = поле.placeholder || "";
        break;
      case "select":
        input = document.createElement("select");
        поле.варианты.forEach((вариант) => {
          const option = document.createElement("option");
          option.value = вариант.значение;
          option.textContent = вариант.text;
          input.appendChild(option);
        });
        break;
      default:
        input = document.createElement("input");
        input.type = поле.тип || "text";
        input.placeholder = поле.placeholder || "";
        if (поле.обязательный) input.required = true;
        break;
    }

    input.id = поле.имя;
    input.name = поле.имя;
    if (поле.значение) input.value = поле.значение;

    group.appendChild(input);
    form.appendChild(group);
  });

  const button = document.createElement("button");
  button.type = "submit";
  button.textContent = "Отправить";
  form.appendChild(button);

  form.addEventListener("submit", (e) => {
    e.preventDefault();

    const data = new FormData(form);
    const dataObject = {};
    data.forEach((значение, ключ) => {
      dataObject[ключ] = значение;
    });

    console.log("Данные формы:", dataObject);
    alert("Форма отправлена!");
  });

  container.appendChild(form);
}

// Использование
const fields = [
  { имя: "имя", метка: "Имя", тип: "text", обязательный: true },
  { имя: "email", метка: "Email", тип: "email", обязательный: true },
  {
    имя: "пол",
    метка: "Пол",
    тип: "select",
    варианты: [
      { значение: "", текст: "Выберите..." },
      { значение: "муж", текст: "Мужской" },
      { значение: "жен", текст: "Женский" },
    ],
  },
  {
    имя: "сообщение",
    метка: "Сообщение",
    тип: "textarea",
    placeholder: "Введите сообщение...",
  },
];

const container = document.querySelector("#form-container");
createDynamicForm(fields, container);
```

## 🚨 Частые ошибки новичков

### ❌ Работа с пустыми результатами

```javascript
const element = document.querySelector(".несуществующий");

// ❌ ПЛОХО - element может быть null
element.textContent = "Привет"; // Ошибка!

// ✅ ХОРОШО - всегда проверяйте наличие
if (element) {
  element.textContent = "Привет";
}
```

### ❌ Неправильное использование querySelectorAll

```javascript
const elements = document.querySelectorAll(".item");

// ❌ ПЛОХО - NodeList не имеет метода push
elements.push(newElement);

// ✅ ХОРОШО - используйте Array.from или spread
const array = Array.from(elements);
array.push(newElement);

// Или используйте forEach для обхода
elements.forEach((element) => {
  element.classList.add("active");
});
```

### ❌ Опасное использование innerHTML

```javascript
const container = document.querySelector(".container");
const userInput = "<script>alert('xss')</script>";

// ❌ ОПАСНО - XSS атака!
container.innerHTML = userInput;

// ✅ БЕЗОПАСНО - используйте textContent
container.textContent = userInput;

// Или создавайте elements безопасно
const element = document.createElement("div");
element.textContent = userInput;
container.appendChild(element);
```

### ❌ Забытый cloneNode

```javascript
const template = document.querySelector("#template");

// ❌ ПЛОХО - перемещаем element
container.appendChild(template);

// ✅ ХОРОШО - клонируем element
const copy = template.cloneNode(true);
container.appendChild(copy);
```

## 📚 Шпаргалка быстрых операций

| Задача                | Метод                  | Пример                                 |
| --------------------- | ---------------------- | -------------------------------------- |
| Найти element         | `querySelector()`      | `document.querySelector(".btn")`       |
| Найти много элементов | `querySelectorAll()`   | `document.querySelectorAll("div")`     |
| Создать element       | `createElement()`      | `document.createElement("div")`        |
| Добавить в конец      | `append()`             | `parent.append(child)`                 |
| Добавить в начало     | `prepend()`            | `parent.prepend(child)`                |
| Заменить element      | `replaceWith()`        | `old.replaceWith(new)`                 |
| Удалить element       | `remove()`             | `element.remove()`                     |
| Добавить класс        | `classList.add()`      | `element.classList.add("active")`      |
| Удалить класс         | `classList.remove()`   | `element.classList.remove("active")`   |
| Переключить класс     | `classList.toggle()`   | `element.classList.toggle("visible")`  |
| Проверить класс       | `classList.contains()` | `element.classList.contains("active")` |
| Изменить стиль        | `style`                | `element.style.color = "red"`          |
| Получить стиль        | `getComputedStyle()`   | `getComputedStyle(element)`            |

## 🎮 Практика в консоли

Открой F12 на любой странице и попробуй:

```javascript
// 1. Найти elements
const headers = document.querySelectorAll("h1, h2, h3");
console.log(`Найдено заголовков: ${headers.length}`);

// 2. Создать newElement element
const button = document.createElement("button");
button.textContent = "Новая button";
button.className = "my-button";
button.style.backgroundColor = "#007bff";
button.style.color = "white";
button.style.border = "none";
button.style.padding = "10px 20px";

// 3. Добавить на страницу
document.body.prepend(button);

// 4. Добавить действие
button.addEventListener("click", () => {
  const randomColor =
    "#" + Math.floor(Math.random() * 16777215).toString(16);
  document.body.style.backgroundColor = randomColor;
  button.textContent = `Цвет: ${randomColor}`;
});

// 5. Работа с существующими элементами
const allParagraphs = document.querySelectorAll("p");
allParagraphs.forEach((paragraph, index) => {
  paragraph.style.borderLeft = "3px solid #007bff";
  paragraph.style.paddingLeft = "10px";
  paragraph.setAttribute("data-index", index);
});

// 6. Создать list
const list = document.createElement("ul");
for (let i = 1; i <= 5; i++) {
  const element = document.createElement("li");
  element.textContent = `Элемент ${i}`;
  element.style.cursor = "pointer";
  element.addEventListener("click", function () {
    this.style.backgroundColor = this.style.backgroundColor ? "" : "#f0f0f0";
  });
  list.appendChild(element);
}
document.body.append(list);
```

---

**Запомни главное:** DOM - это мост между HTML и JavaScript! Он позволяет динамически изменять веб-страницы и создавать интерактивные интерфейсы. 🌉

Используй `querySelector()` для поиска, `classList` для классов, и всегда проверяйте существование элементов! 🎯
