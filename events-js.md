# События в JavaScript 🎪

## 🎦 Что такое события?

Представь события как **сигналы в реальном мире**:

🚨 **Дымовой датчик** = сигнализирует о дыме  
🔔 **Дверной звонок** = сообщает о гостях  
🎯 **Светофор** = показывает когда можно ехать

```javascript
// JavaScript ждёт сигналов и реагирует на них
const button = document.createElement("button");
button.textContent = "Нажми меня";
document.body.appendChild(button);
button.addEventListener("click", () => {
  console.log("Кнопка нажата!");
});
```

Примеры выполняются в браузере на учебной HTML-странице. Сначала создайте элементы с указанными селекторами или измените селекторы под свою разметку. querySelector возвращает null, если элемент не найден. Самостоятельные блоки запускайте отдельно; примеры с ❌ намеренно показывают неверный приём.

## 🎯 addEventListener() - основной способ

### 🔧 Базовый синтаксис

```javascript
const element = document.querySelector(".my-button");

element.addEventListener("событие", functionHandler);

// Пример
element.addEventListener("click", function () {
  alert("Кнопка нажата!");
});
```

### 🎯 Разные способы назначить событие

```javascript
const button = document.querySelector("#my-button");

// 1. addEventListener (рекомендуется)
button.addEventListener("click", () => {
  console.log("Способ 1: addEventListener");
});

// 2. Свойство элемента (старый способ)
button.onclick = () => {
  console.log("Способ 2: свойство onclick");
};

// 3. Атрибут в HTML (не рекомендуется)
// <button onclick="alert('Привет!')">Нажми</button>
```

### 🎯 Несколько обработчиков

```javascript
button.addEventListener("click", () => console.log("Первый обработчик"));
button.addEventListener("click", () => console.log("Второй обработчик"));

// Оба сработают!
```

## 🖱️ Мышьиные события

### 👆 Основные события мыши

```javascript
const element = document.querySelector(".box");

// Нажатие кнопки мыши
element.addEventListener("mousedown", () => {
  console.log("Кнопка нажата");
});

// Отпускание кнопки мыши
element.addEventListener("mouseup", () => {
  console.log("Кнопка отпущена");
});

// Полный клик (mousedown + mouseup)
element.addEventListener("click", () => {
  console.log("Клик!");
});

// Двойной клик
element.addEventListener("dblclick", () => {
  console.log("Двойной клик!");
});
```

### 👆 Движение мыши

```javascript
const element = document.querySelector(".area");

// Мышь вошла в элемент
element.addEventListener("mouseenter", () => {
  element.style.backgroundColor = "lightblue";
});

// Мышь ушла из элемента
element.addEventListener("mouseleave", () => {
  element.style.backgroundColor = "transparent";
});

// Движение внутри элемента
element.addEventListener("mousemove", (e) => {
  const coordinates = `X: ${e.clientX}, Y: ${e.clientY}`;
  element.textContent = coordinates;
});
```

### 👆 Контекстное меню

```javascript
const image = document.querySelector("img");

// Отключаем контекстное меню на изображении
image.addEventListener("contextmenu", (e) => {
  e.preventDefault(); // Отменяем стандартное меню
  console.log("Контекстное меню отключено");
});
```

## ⌨️ Клавиатурные события

### 🎹 Основные события клавиатуры

```javascript
const field = document.querySelector("input");

// Нажатие клавиши
field.addEventListener("keydown", (e) => {
  console.log(`Нажата клавиша: ${e.key}`);
  console.log(`Физическая клавиша: ${e.code}`);
});

// Отпускание клавиши
field.addEventListener("keyup", (e) => {
  console.log(`Отпущена клавиша: ${e.key}`);
});

// Изменение текста: учитывает вставку и способы ввода без клавиш.
field.addEventListener("input", (e) => {
  console.log(`Текущее значение: ${e.target.value}`);
});
// keypress устарел; для клавиш используйте keydown/keyup.
```

### 🎹 Специальные клавиши

```javascript
document.addEventListener("keydown", (e) => {
  // Ctrl, Alt, Shift, Meta (Cmd на Mac)
  if (e.ctrlKey && e.key === "s") {
    e.preventDefault();
    console.log("Сохранить (Ctrl+S)");
  }

  if (e.key === "Escape") {
    console.log("Нажат Escape");
  }

  if (e.key === "Enter") {
    console.log("Нажат Enter");
  }

  // Стрелки
  if (e.key.startsWith("Arrow")) {
    console.log(`Нажата стрелка: ${e.key}`);
  }
});
```

## 📄 События форм

### 📝 Формы и поля ввода

```javascript
const form = document.querySelector("form");
const input = document.querySelector("input[name='email']");

// Отправка формы
form.addEventListener("submit", (e) => {
  e.preventDefault(); // Предотвращаем отправку

  const email = input.value;
  console.log(`Отправлен email: ${email}`);
});

// Изменение значения (когда поле теряет фокус)
input.addEventListener("change", (e) => {
  console.log(`Email изменен на: ${e.target.value}`);
});

// Ввод текста в реальном времени
input.addEventListener("input", (e) => {
  console.log(`Текущий email: ${e.target.value}`);
});

// Получение фокуса
input.addEventListener("focus", () => {
  input.style.borderColor = "blue";
});

// Потеря фокуса
input.addEventListener("blur", () => {
  input.style.borderColor = "gray";
});
```

### 📝 Валидация форм

```javascript
const form = document.querySelector(".registration-form");

form.addEventListener("submit", (e) => {
  const errors = [];

  // Проверка полей
  const name = form.querySelector('[name="name"]').value.trim();
  const email = form.querySelector('[name="email"]').value.trim();
  const password = form.querySelector('[name="password"]').value;

  if (name.length < 2) {
    errors.push("Имя должно содержать минимум 2 символа");
  }

  if (!email.includes("@")) {
    errors.push("Введите корректный email");
  }

  if (password.length < 6) {
    errors.push("Пароль должен содержать минимум 6 символов");
  }

  // Если есть ошибки - отменяем отправку
  if (errors.length > 0) {
    e.preventDefault();
    alert(errors.join("\n"));
  } else {
    console.log("Форма валидна, отправляем...");
  }
});
```

## 🖥️ События окна и документа

### 📏 Изменение размера окна

```javascript
window.addEventListener("resize", () => {
  const width = window.innerWidth;
  const height = window.innerHeight;
  console.log(`Размер окна: ${width}x${height}`);
});
```

### 📜 Прокрутка страницы

```javascript
window.addEventListener("scroll", () => {
  const scroll = window.scrollY;

  // Кнопка "Наверх" при прокрутке
  const scrollTopBtn = document.querySelector("#scroll-top");
  if (scrollTopBtn) {
    scrollTopBtn.style.display = scroll > 300 ? "block" : "none";
  }
});
```

### 📗 Загрузка страницы

```javascript
// DOM загружен (лучший способ для манипуляции с DOM)
document.addEventListener("DOMContentLoaded", () => {
  console.log("DOM полностью загружен");
  // Здесь безопасно работать с элементами
});

// Все ресурсы загружены (включая изображения, стили)
window.addEventListener("load", () => {
  console.log("Страница полностью загружена");
});

// Состояние приложения: меняйте при редактировании и сохранении.
let hasUnsavedChanges = false;
// Перед закрытием страницы
window.addEventListener("beforeunload", (e) => {
  // Предупреждение при несохраненных данных
  if (hasUnsavedChanges) {
    e.preventDefault();
    e.returnValue = ""; // Совместимость; свой текст браузер не показывает
  }
});
```

## 🎯 Объект события (Event)

### 📊 Основные свойства

```javascript
const button = document.querySelector(".btn");

button.addEventListener("click", (e) => {
  console.log("Тип события:", e.type); // "click"
  console.log("Целевой элемент:", e.target); // Элемент клика: может быть вложенным элементом кнопки
  console.log("Текущий элемент:", e.currentTarget); // button
  console.log("Время события:", e.timeStamp); // timestamp
});
```

### 🖱️ Координаты мыши

```javascript
document.addEventListener("click", (e) => {
  // Относительно окна браузера
  console.log("clientX:", e.clientX, "clientY:", e.clientY);

  // Относительно всего документа (с учетом прокрутки)
  console.log("pageX:", e.pageX, "pageY:", e.pageY);

  // Относительно экрана
  console.log("screenX:", e.screenX, "screenY:", e.screenY);
});
```

### 🎹 Информация о клавише

```javascript
document.addEventListener("keydown", (e) => {
  console.log("Клавиша:", e.key); // "a", "Enter", "Escape"
  console.log("Код:", e.code); // "KeyA", "Enter", "Escape"
  // keyCode, which и keypress устарели. Используйте key/code и keydown/keyup.

  // Модификаторы
  console.log("Ctrl:", e.ctrlKey);
  console.log("Alt:", e.altKey);
  console.log("Shift:", e.shiftKey);
  console.log("Meta:", e.metaKey); // Cmd на Mac
});
```

## 🎯 Управление событиями

### 🛑 Предотвращение действия по умолчанию

```javascript
// Отменить переход по ссылке
const link = document.querySelector("a");
link.addEventListener("click", (e) => {
  e.preventDefault();
  console.log("Переход отменен");
});

// Отправить форму через AJAX
const form = document.querySelector("form");
form.addEventListener("submit", (e) => {
  e.preventDefault();
  // Отправляем данные через fetch
});
```

### 🛑 Остановка всплытия событий

```html
<div class="outer">
    <div class="middle">
        <div class="inner">Кликни меня</div>
    </div>
</div>

<script>
const inner = document.querySelector(".inner");
const middle = document.querySelector(".middle");
const outer = document.querySelector(".outer");

inner.addEventListener("click", (e) => {
    console.log("Внутренний элемент");
    e.stopPropagation(); // Останавливаем всплытие
});

middle.addEventListener("click", () => {
    console.log("Средний элемент"); // Не выполнится
});

outer.addEventListener("click", () => {
    console.log("Внешний элемент"); // Не выполнится
});
</script>
```

### 🧹 Удаление обработчика

```javascript
const button = document.querySelector(".btn");

function handler() {
  console.log("Кнопка нажата!");
}

// Добавляем обработчик
button.addEventListener("click", handler);

// Удаляем обработчик (та же самая функция)
button.removeEventListener("click", handler);
```

### 🎯 Делегирование событий

```javascript
// Вместо этого (плохо для многих элементов)
const buttons = document.querySelectorAll(".btn");
buttons.forEach((button) => {
  button.addEventListener("click", () => {
    console.log("Кнопка нажата");
  });
});

// Используем делегирование (хорошо)
const container = document.querySelector(".buttons-container");
container.addEventListener("click", (e) => {
  if (e.target.classList.contains("btn")) {
    console.log(`Нажата кнопка: ${e.target.textContent}`);
  }
});
```

## 🎯 Практические примеры

### 🎨 Перетаскивание (Drag & Drop)

```javascript
const element = document.querySelector(".draggable");
let isDragging = false;
let offsetX = 0;
let offsetY = 0;

element.addEventListener("mousedown", (e) => {
  isDragging = true;

  const rect = element.getBoundingClientRect();
  offsetX = e.clientX - rect.left;
  offsetY = e.clientY - rect.top;

  element.style.position = "fixed"; // clientX/clientY относятся к окну
  element.style.zIndex = "1000";
});

document.addEventListener("mousemove", (e) => {
  if (!isDragging) return;

  element.style.left = `${e.clientX - offsetX}px`;
  element.style.top = `${e.clientY - offsetY}px`;
});

document.addEventListener("mouseup", () => {
  isDragging = false;
  element.style.zIndex = "";
});
```

### 🎮 Игра "Поймай кружок"

```javascript
const gameField = document.querySelector(".game-field");
let score = 0;
let time = 30;

function createCircle() {
  const circle = document.createElement("div");
  circle.className = "circle";

  // Случайные координаты
  const maxX = gameField.clientWidth - 50;
  const maxY = gameField.clientHeight - 50;
  circle.style.left = Math.random() * maxX + "px";
  circle.style.top = Math.random() * maxY + "px";

  // Случайный цвет
  circle.style.backgroundColor = `hsl(${Math.random() * 360}, 70%, 60%)`;

  circle.addEventListener("click", () => {
    score++;
    document.querySelector("#score").textContent = score;
    circle.remove();
  });

  gameField.appendChild(circle);

  // Удалить через случайное время
  setTimeout(
    () => {
      if (circle.parentNode) {
        circle.remove();
      }
    },
    Math.random() * 2000 + 1000,
  );
}

// Игровой цикл
const interval = setInterval(() => {
  if (time <= 0) {
    clearInterval(interval);
    alert(`Игра окончена! Счет: ${score}`);
    return;
  }

  time--;
  document.querySelector("#timer").textContent = time;
  createCircle();
}, 1000);
```

### 📝 Живой поиск

```javascript
const search = document.querySelector("#search");
const results = document.querySelector("#search-results");

let searchVersion = 0;
search.addEventListener("input", async (e) => {
  const version = ++searchVersion;
  const query = e.target.value.trim();

  if (query.length < 2) {
    results.innerHTML = "";
    return;
  }

  // Показываем индикатор загрузки
  results.innerHTML = "<div class='loading'>Поиск...</div>";

  try {
    // Симуляция API запроса
    await new Promise((resolve) => setTimeout(resolve, 300));

    if (version !== searchVersion) return; // Устаревший ответ не обновляет экран
    // Пример данных
    const data = ["JavaScript", "Java", "Python", "TypeScript"];

    const filtered = data.filter((item) =>
      item.toLowerCase().includes(query.toLowerCase()),
    );

    if (filtered.length === 0) {
      results.innerHTML = "<div class='no-results'>Ничего не найдено</div>";
    } else {
      results.innerHTML = filtered
        .map((item) => `<div class='result-item'>${item}</div>`)
        .join("");

      // Добавляем обработчики на результаты
      results.querySelectorAll(".result-item").forEach((item) => {
        item.addEventListener("click", () => {
          search.value = item.textContent;
          results.innerHTML = "";
        });
      });
    }
  } catch (error) {
    if (version !== searchVersion) return;
    results.innerHTML = "<div class='error'>Ошибка поиска</div>";
  }
});

// Закрывать результаты при клике вне
document.addEventListener("click", (e) => {
  if (!e.target.closest("#search-container")) {
    searchVersion++; // Не показывать старый ответ после закрытия
    results.innerHTML = "";
  }
});
```

### 🎵 Музыкальный плеер

```javascript
const playBtn = document.querySelector("#play");
const pauseBtn = document.querySelector("#pause");
const progress = document.querySelector("#progress");
const time = document.querySelector("#time");
const audio = new Audio("music.mp3");

playBtn.addEventListener("click", () => {
  audio.play().catch((error) => console.error("Воспроизведение не началось:", error.message));
});

pauseBtn.addEventListener("click", () => {
  audio.pause();
});

// Обновление прогресса
audio.addEventListener("timeupdate", () => {
  if (!Number.isFinite(audio.duration) || audio.duration <= 0) return;
  const progressPercent = (audio.currentTime / audio.duration) * 100;
  progress.value = progressPercent;

  const currentTime = formatTime(audio.currentTime);
  const totalTime = formatTime(audio.duration);
  time.textContent = `${currentTime} / ${totalTime}`;
});

progress.addEventListener("input", () => {
  if (Number.isFinite(audio.duration) && audio.duration > 0) {
    audio.currentTime = (progress.value / 100) * audio.duration;
  }
});

audio.addEventListener("ended", () => {
  playBtn.textContent = "Слушать снова";
});

function formatTime(seconds) {
  if (!Number.isFinite(seconds) || seconds < 0) return "--:--";
  const minutes = Math.floor(seconds / 60);
  const secs = Math.floor(seconds % 60);
  return `${minutes}:${secs.toString().padStart(2, "0")}`;
}
```

## 🚨 Частые ошибки новичков

### ❌ Несколько обработчиков на один элемент

```javascript
const button = document.querySelector(".btn");

// ❌ ПЛОХО - обработчик добавляется каждый раз
initFunction();
initFunction(); // Два обработчика!

function initFunction() {
  button.addEventListener("click", () => console.log("Клик"));
}

// ✅ ХОРОШО - проверяем наличие обработчика
if (!button.dataset.initialized) {
  button.addEventListener("click", () => console.log("Клик"));
  button.dataset.initialized = "true";
}
```

### ❌ Забытый preventDefault

```javascript
const form = document.querySelector("form");

// ❌ ПЛОХО - форма отправится стандартным способом
form.addEventListener("submit", () => {
  // AJAX запрос
});

// ✅ ХОРОШО - отменяем стандартное поведение
form.addEventListener("submit", (e) => {
  e.preventDefault();
  // AJAX запрос
});
```

### 🔍 Удаление из DOM не уничтожает объект

```javascript
const button = document.querySelector(".btn");

button.addEventListener("click", () => {
  button.remove(); // Элемент удален
  button.textContent = "Новый текст"; // Допустимо: объект существует, но уже не виден в документе
  console.log(button.isConnected); // false
});
```

### ❌ Отсутствие делегирования для динамических элементов

```javascript
// ❌ ПЛОХО - обработчики не работают на новых элементах
добавить_кнопки();
document.querySelectorAll(".btn").forEach((btn) => {
  btn.addEventListener("click", handleClick);
});
добавить_еще_кнопки(); // У новых кнопок обработчиков нет!

// ✅ ХОРОШО - используем делегирование
document.querySelector(".container").addEventListener("click", (e) => {
  if (e.target.classList.contains("btn")) {
    handleClick(e);
  }
});
```

## 📚 Шпаргалка быстрых событий

| Тип события       | Метод              | Пример                                                   |
| ----------------- | ------------------ | -------------------------------------------------------- |
| Клик мыши         | `click`            | `element.addEventListener("click", handler)`             |
| Двойной клик      | `dblclick`         | `element.addEventListener("dblclick", handler)`          |
| Наведение мыши    | `mouseenter`       | `element.addEventListener("mouseenter", handler)`        |
| Уход мыши         | `mouseleave`       | `element.addEventListener("mouseleave", handler)`        |
| Нажатие клавиши   | `keydown`          | `document.addEventListener("keydown", handler)`          |
| Ввод текста       | `input`            | `input.addEventListener("input", handler)`               |
| Отправка формы    | `submit`           | `form.addEventListener("submit", handler)`               |
| Изменение размера | `resize`           | `window.addEventListener("resize", handler)`             |
| Прокрутка         | `scroll`           | `window.addEventListener("scroll", handler)`             |
| Загрузка DOM      | `DOMContentLoaded` | `document.addEventListener("DOMContentLoaded", handler)` |

## 🎮 Практика в консоли

Открой F12 на любой странице и попробуй:

```javascript
// 1. Следим за кликами
document.addEventListener("click", (e) => {
  console.log("Кликнут элемент:", e.target.tagName);
  console.log("Координаты:", e.clientX, e.clientY);
});

// 2. Следим за наведением
const allLinks = document.querySelectorAll("a");
allLinks.forEach((link) => {
  link.addEventListener("mouseenter", () => {
    link.style.backgroundColor = "yellow";
  });
  link.addEventListener("mouseleave", () => {
    link.style.backgroundColor = "";
  });
});

// 3. Горячие клавиши
document.addEventListener("keydown", (e) => {
  if (e.ctrlKey && e.key === "k") {
    e.preventDefault();
    console.log("Команда поиска (Ctrl+K)");
  }
});

// 4. Динамическое добавление элементов
const container = document.querySelector("body");
const button = document.createElement("button");
button.textContent = "Добавить параграф";
button.addEventListener("click", () => {
  const paragraph = document.createElement("p");
  paragraph.textContent = `Параграф ${document.querySelectorAll("p").length + 1}`;
  paragraph.style.border = "1px solid #ccc";
  paragraph.style.padding = "10px";
  paragraph.style.margin = "5px 0";
  container.appendChild(paragraph);
});
container.appendChild(button);

// 5. Следим за скроллом
window.addEventListener("scroll", () => {
  const scroll = window.scrollY;
  const height = document.documentElement.scrollHeight - window.innerHeight;
  const progress = height > 0 ? (scroll / height) * 100 : 0;
  console.log(`Прокручено: ${progress.toFixed(1)}%`);
});
```

## 📝 Задания для закрепления

### Задание 1: Кнопка-счётчик
Создай кнопку с текстом "Кликов: 0". При каждом клике число увеличивается на 1 и текст кнопки обновляется.

### Задание 2: Валидация поля ввода
Создай поле ввода `<input>`, которое:
- Подсвечивается зелёной рамкой, если введено 2+ символа
- Подсвечивается красной рамкой, если поле пустое или 1 символ
- Проверка происходит при каждом вводе (событие `input`)

### Задание 3: Горячие клавиши
Добавь обработчик клавиатуры на `document`, который:
- При нажатии `Ctrl+B` переключает класс `bold` на `<body>`
- При нажатии `Ctrl+I` переключает класс `italic` на `<body>`
- Не забудь вызвать `preventDefault()` чтобы не срабатывало стандартное поведение

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** События - это как сигналы в реальном мире! JavaScript может слушать эти сигналы и реагировать на них, делая веб-страницы интерактивными. 🎪

Используй `addEventListener()`, `preventDefault()` для отмены действий и делегирование для динамических элементов! 🎯

---

[⬅️ Предыдущая тема: DOM-манипуляции](dom-manipulation.md) | [📚 Оглавление](README.md) | [Следующая тема: Даты ➡️](dates-js.md)
