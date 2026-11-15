# Обработка ошибок 🛡️

## 🎦 Что такое ошибки?

Представь ошибки как **пробки на дороге**:

🛣️ **Дорога** = выполнение кода  
🚧 **Пробка** = ошибка, которая останавливает движение  
👷 **Дорожный рабочий** = обработчик ошибок  
🔄 **Объезд** = альтернативный путь

```javascript
try {
  // Пытаемся проехать по дороге
  рискованный_код();
} catch (ошибка) {
  // Пробка! Ищем объезд
  console.log("Ошибка:", ошибка.message);
}
```

## 🛑 try...catch - основа обработки ошибок

### 🎯 Базовый синтаксис

```javascript
try {
  // Код, который может вызвать ошибку
  const result = riskyOperation();
  console.log("Результат:", result);
} catch (ошибка) {
  // Что делать, если произошла ошибка
  console.error("Произошла ошибка:", ошибка.message);
  console.error("Тип ошибки:", ошибка.name);
  console.error("Стек вызовов:", ошибка.stack);
} finally {
  // Выполнится всегда (и при успехе, и при ошибке)
  console.log("Блок finally выполнен");
}
```

### 🎯 Простые примеры

```javascript
// 1. Деление на ноль
try {
  const result = 10 / 0; // Infinity, но не ошибка
  console.log("Результат:", result);
} catch (error) {
  console.error("Ошибка:", error);
}

// 2. Доступ к несуществующему свойству
try {
  const object = null;
  console.log(object.property); // TypeError
} catch (error) {
  console.error("Невозможно получить свойство:", error.message);
}

// 3. Парсинг JSON
try {
  const invalidJson = "{ некорректный: json }";
  const data = JSON.parse(invalidJson); // SyntaxError
} catch (error) {
  console.error("Ошибка парсинга JSON:", error.message);
}
```

## 🎯 Создание собственных ошибок

### 🎯 throw - генерация ошибки

```javascript
function checkAge(age) {
  if (!Number.isFinite(age)) {
    throw new TypeError("Возраст должен быть числом");
  }

  if (age < 0) {
    throw new RangeError("Возраст не может быть отрицательным");
  }

  if (age > 120) {
    throw new RangeError("Возраст слишком большой");
  }

  return "Возраст корректен";
}

try {
  console.log(checkAge(25)); // "Возраст корректен"
  console.log(checkAge(-5)); // Ошибка!
} catch (error) {
  console.error("Ошибка в возрасте:", error.message);
  console.error("Тип ошибки:", error.name);
}
```

### 🎯 Класс Error и его наследники

```javascript
const error = new Error("Что-то пошло не так");
console.log(error.name); // "Error"
console.log(error.message); // "Что-то пошло не так"

class CustomError extends Error {
  constructor(message, code) {
    super(message);
    this.name = "CustomError";
    this.code = code;
  }
}
const myError = new CustomError("Неверный логин", "AUTH_001");
console.log(myError.message); // "Неверный логин"
console.log(myError.code); // "AUTH_001"
// Другие встроенные классы: TypeError, RangeError, SyntaxError, ReferenceError.
```

## 🌐 try...catch с асинхронным кодом

### 🎯 Асинхронные функции

```javascript
async function loadData(url) {
  try {
    const response = await fetch(url);

    if (!response.ok) {
      throw new Error(`HTTP ошибка: ${response.status}`);
    }

    const data = await response.json();
    return data;
  } catch (error) {
    console.error("Ошибка загрузки данных:", error.message);
    return null; // Возвращаем null при ошибке
  }
}

// Использование
(async () => {
  const data = await loadData(
    "https://jsonplaceholder.typicode.com/users/1",
  );
  if (data) {
    console.log("Данные загружены:", data);
  } else {
    console.log("Не удалось загрузить data");
  }
})();
```

### 🎯 Промисы с catch

```javascript
function loadUser(id) {
  return fetch(`https://jsonplaceholder.typicode.com/users/${id}`)
    .then((response) => {
      if (!response.ok) {
        throw new Error(`HTTP ${response.status}`);
      }
      return response.json();
    })
    .catch((error) => {
      console.error("Ошибка в промисе:", error.message);
      throw error; // Пробрасываем дальше
    });
}

// Использование
loadUser(1)
  .then((user) => console.log("Пользователь:", user))
  .catch((error) => console.error("Финальная ошибка:", error.message));
```

## 🎯 Вложенные блоки try...catch

```javascript
function processFile(path) {
  try {
    console.log("Открываем файл:", path);

    try {
      const content = readFile(path);
      console.log("Файл прочитан");

      try {
        const data = JSON.parse(content);
        console.log("JSON распарсен:", data);
      } catch (jsonError) {
        console.error("Ошибка парсинга JSON:", jsonError.message);
        throw new Error("Некорректный формат JSON в файле");
      }
    } catch (readError) {
      console.error("Ошибка чтения файла:", readError.message);
      throw new Error("Не удалось прочитать файл");
    }
  } catch (generalError) {
    console.error("Общая ошибка обработки:", generalError.message);
    return false;
  }
}

// Упрощенная версия с одним try...catch
function processFileImproved(path) {
  try {
    console.log("Открываем файл:", path);
    const content = readFile(path);
    console.log("Файл прочитан");

    const data = JSON.parse(content);
    console.log("JSON распарсен:", data);
    return data;
  } catch (error) {
    if (error instanceof SyntaxError) {
      console.error("Ошибка парсинга JSON:", error.message);
    } else {
      console.error("Ошибка чтения файла:", error.message);
    }
    return false;
  }
}
```

## 🎯 Практические паттерны обработки ошибок

### 🎯 Валидация данных

```javascript
class ValidationError extends Error {
  constructor(field, message) {
    super(`${field}: ${message}`);
    this.name = "ValidationError";
    this.field = field;
  }
}
function validateUser(user) {
  if (typeof user.name !== "string" || user.name.trim().length < 2) {
    throw new ValidationError("name", "Минимум 2 символа");
  }
  if (typeof user.email !== "string" || !user.email.includes("@")) {
    throw new ValidationError("email", "Нужен символ @");
  }
  if (!Number.isFinite(user.age) || user.age < 18) {
    throw new ValidationError("age", "Минимум 18 лет");
  }
  return true;
}
try {
  validateUser({ name: "А", email: "неверный-email", age: 16 });
} catch (error) {
  if (error instanceof ValidationError) console.error(error.message);
  else throw error;
}
// Проверка email здесь иллюстрирует ветвление, а не полную проверку адреса.
```

### 🎯 Обработка ошибок API

```javascript
class APIError extends Error {
  constructor(status, message) {
    super(message);
    this.name = "APIError";
    this.status = status;
  }
}
async function apiRequest(url, options = {}) {
  const headers = new Headers(options.headers);
  if (!headers.has("Content-Type")) headers.set("Content-Type", "application/json");
  let response;
  try {
    response = await fetch(url, { ...options, headers });
  } catch (error) {
    throw new APIError(0, `Сетевой запрос не выполнен: ${error.message}`);
  }
  if (!response.ok) throw new APIError(response.status, `HTTP ${response.status}`);
  if (response.status === 204) return null; // Нет тела ответа
  return response.json(); // Ошибка JSON остаётся ошибкой разбора, а не HTTP 500
}
async function getUser(id) {
  try {
    return await apiRequest(`https://jsonplaceholder.typicode.com/users/${id}`);
  } catch (error) {
    if (error instanceof APIError) console.error(error.status, error.message);
    else console.error("Не удалось прочитать JSON:", error.message);
    return null;
  }
}
```

### 🎯 Graceful degradation (плавное ухудшение)

```javascript
class ResilientLoader {
  constructor(primaryUrl, backupUrls = []) {
    this.primaryUrl = primaryUrl;
    this.backupUrls = backupUrls;
    this.timeout = 5000;
  }
  async loadWithTimeout(url) {
    const controller = new AbortController();
    const timer = setTimeout(() => controller.abort(), this.timeout);
    try {
      const response = await fetch(url, { signal: controller.signal });
      if (!response.ok) throw new Error(`HTTP ${response.status}`);
      return await response.json();
    } finally {
      clearTimeout(timer);
    }
  }
  async load() {
    for (const url of [this.primaryUrl, ...this.backupUrls]) {
      try {
        return await this.loadWithTimeout(url);
      } catch (error) {
        console.warn(`Источник ${url} недоступен:`, error.message);
      }
    }
    return { status: "offline", data: null };
  }
}
// Укажите собственные адреса источников. Сеть отменяется через AbortController;
// Promise.race сам по себе только выбирает первый результат и не отменяет fetch.
const loader = new ResilientLoader("https://jsonplaceholder.typicode.com/users/1");
loader.load().then(console.log).catch(console.error);
```

## 🔀 error object - структура ошибки

### 🎯 Основные свойства

```javascript
try {
  // Код вызывающий ошибку
  JSON.parse("{некорректный json}");
} catch (ошибка) {
  console.log("Имя ошибки:", ошибка.name); // "SyntaxError"
  console.log("Сообщение:", ошибка.message); // Текст сообщения зависит от движка и версии
  console.log("Стек вызовов:", ошибка.stack); // Полный стек вызовов

  // Полный объект ошибки
  console.log("Полная ошибка:", ошибка);
}
```

### 🎯 Собственные свойства ошибок

```javascript
class BusinessError extends Error {
  constructor(code, message, details = {}) {
    super(message);
    this.name = "BusinessError";
    this.code = code;
    this.details = details;
    this.time = new Date().toISOString();
  }
  toObject() {
    return { name: this.name, code: this.code, message: this.message, details: this.details, time: this.time };
  }
}
const businessError = new BusinessError("PAYMENT_FAILED", "Платёж не прошёл", { amount: 1000 });
console.log(businessError.toObject()); // Время зависит от момента запуска
```

## 🎯 Глобальная обработка ошибок

### 🎯 window.onerror - синхронные ошибки

```javascript
window.onerror = function (
  сообщение,
  источник,
  номер_строки,
  номер_колонки,
  ошибка,
) {
  console.error("Глобальная ошибка:", {
    сообщение,
    источник,
    номер_строки,
    номер_колонки,
    ошибка: ошибка?.stack,
  });

  // Прикладное журналирование: в этом примере только выводим данные.
  console.error({
    тип: "синхронная",
    сообщение,
    источник,
    номер_строки,
    номер_колонки,
    стек: ошибка?.stack,
    пользователь: null, // Приложение может добавить разрешённый контекст
    время: new Date().toISOString(),
  });

  // Не предотвращаем стандартное поведение
  return false;
};
```

### 🎯 window.onunhandledrejection - необработанные промисы

```javascript
window.onunhandledrejection = function (событие) {
  console.error("Необработанный промис:", событие.reason);

  console.error({
    тип: "промис",
    причина: событие.reason,
    пользователь: null,
    время: new Date().toISOString(),
  });

  // Предотвращаем вывод ошибки в консоль
  событие.preventDefault();
};
```

### 🎯 try...catch на уровне модуля

```javascript
// error-handler.js
class МенеджерОшибок {
  constructor() {
    this.ошибки = [];
    this.настроить_глобальные_обработчики();
  }

  настроить_глобальные_обработчики() {
    window.onerror = (
      сообщение,
      источник,
      номер_строки,
      номер_колонки,
      ошибка,
    ) => {
      this.записать_ошибку({
        тип: "синхронная",
        сообщение,
        источник,
        номер_строки,
        номер_колонки,
        ошибка,
        время: new Date(),
      });
      return false;
    };

    window.onunhandledrejection = (событие) => {
      this.записать_ошибку({
        тип: "промис",
        причина: событие.reason,
        время: new Date(),
      });
      событие.preventDefault();
    };
  }

  записать_ошибку(ошибка) {
    this.ошибки.push(ошибка);
    console.error("Зарегистрирована ошибка:", ошибка);

    // Отправляем на сервер
    this.отправить_на_сервер(ошибка);
  }

  отправить_на_сервер(ошибка) {
    // В реальном приложении здесь был бы fetch
    console.log("Отправка ошибки на сервер:", ошибка);
  }

  получить_ошибки() {
    return [...this.ошибки];
  }

  очистить_ошибки() {
    this.ошибки = [];
  }
}

// Создаем глобальный экземпляр
window.менеджер_ошибок = new МенеджерОшибок();
```

## 🚨 Частые ошибки новичков

### ❌ Забытый catch

```javascript
// ❌ ПЛОХО - ошибка не обработана
async function loadData() {
    const data = await fetch('/api/data'); // Может вызвать ошибку
    return data.json(); // Тоже может вызвать ошибку
}

// ✅ ХОРОШО - обрабатываем ошибки
async function loadData() {
    try {
        const response = await fetch('/api/data');
        const data = await response.json();
        return data;
    } catch (ошибка) {
        console.error("Ошибка загрузки:", ошибка);
        return null;
    }
}
```

### ❌ Слишком широкий catch

```javascript
// ❌ ПЛОХО - ловим все ошибки подряд
try {
  // Много разного кода
} catch (ошибка) {
  console.log("Произошла ошибка"); // Непонятно какая именно
}

// ✅ ХОРОШО - специфичная обработка
try {
  // Код работы с файлом
} catch (ошибка) {
  if (ошибка.code === "ENOENT") {
    console.error("Файл не найден");
  } else if (ошибка.code === "EACCES") {
    console.error("Нет доступа к файлу");
  } else {
    console.error("Другая ошибка файла:", ошибка.message);
  }
}
```

### ❌ Игнорирование finally

```javascript
function withResource(work) {
  const resource = { closed: false };
  try {
    return work(resource);
  } catch (error) {
    console.error("Ошибка:", error.message);
    return null;
  } finally {
    resource.closed = true; // Очистка выполняется и при return, и при throw
    console.log("Ресурс очищен:", resource.closed);
  }
}
withResource(() => { throw new Error("Не удалось выполнить операцию"); });
```

### ❌ Неправильное использование throw

```javascript
// Неудачный вариант: выброшенный примитив не имеет обычных свойств Error.
function checkValueBad(value) {
  if (!value) throw "Пустое значение";
  if (typeof value !== "string") throw 1;
}
// Исправленный вариант — отдельная функция, её проверки достижимы.
function checkValue(value) {
  if (typeof value !== "string") throw new TypeError("Значение должно быть строкой");
  if (value === "") throw new Error("Значение не может быть пустым");
  return value;
}
```

## 📚 Шпаргалка обработки ошибок

| Тип ошибки     | Когда использовать              | Пример                                 |
| -------------- | ------------------------------- | -------------------------------------- |
| `try/catch`    | Блок кода с возможными ошибками | `try { risky() } catch(e) { ... }`     |
| `throw`        | Генерация ошибки                | `throw new Error("Произошла ошибка")`  |
| `finally`      | Код, который выполнится всегда  | `try { ... } finally { cleanup() }`    |
| `Error`        | Базовая ошибка                  | `new Error("Сообщение")`               |
| `TypeError`    | Неверный тип данных             | `new TypeError("Ожидается число")`     |
| `RangeError`   | Значение вне диапазона          | `new RangeError("Значение > 100")`     |
| `SyntaxError`  | Синтаксическая ошибка           | `new SyntaxError("Некорректный JSON")` |
| `Custom Error` | Специфические ошибки            | `class MyError extends Error`          |

## 🎮 Практика в консоли

Открой F12 и попробуй:

```javascript
// 1. Базовый try/catch
try {
  JSON.parse("{ некорректный json }");
} catch (ошибка) {
  console.log("Поймали ошибку:", ошибка.message);
  console.log("Тип:", ошибка.name);
}

// 2. Собственная ошибка
function checkNumber(number) {
  if (typeof number !== "number" || isNaN(number)) {
    throw new TypeError("Ожидается число");
  }
  return "Число корректно";
}

try {
  checkNumber("не число");
} catch (error) {
  console.error("Ошибка:", error.message);
}

// 3. Несколько типов ошибок
try {
  const obj = null;
  obj.property.method();
} catch (ошибка) {
  if (ошибка instanceof TypeError) {
    console.log("TypeError: проблема с типом");
  } else if (ошибка instanceof ReferenceError) {
    console.log("ReferenceError: объект не найден");
  } else {
    console.log("Другая ошибка:", ошибка.name);
  }
}

// 4. Finally блок
let resource = "ресурс создан";
try {
  console.log("Работаем с ресурсом");
  throw new Error("Что-то пошло не так");
} catch (error) {
  console.log("Ошибка обработана:", error.message);
} finally {
  resource = "ресурс очищен";
  console.log("Finally:", resource);
}

// 5. Асинхронная ошибка
async function asyncError() {
  try {
    // Симуляция ошибки сети
    throw new Error("Ошибка сети");
  } catch (ошибка) {
    console.log("Асинхронная ошибка:", ошибка.message);
  }
}

asyncError();

// 6. Кастомная ошибка
class ValidationError extends Error {
  constructor(field, message) {
    super(`${field}: ${message}`);
    this.name = "ValidationError";
    this.field = field;
  }
}

function validate(email) {
  if (!email.includes("@")) {
    throw new ValidationError("email", "Некорректный email");
  }
  return "Email валиден";
}

try {
  validate("неправильный-email");
} catch (error) {
  if (error instanceof ValidationError) {
    console.log(`Ошибка в поле "${error.field}": ${error.message}`);
  }
}

// 7. Глобальная ошибка (временно)
const oldHandler = window.onerror;
window.onerror = function (msg, source, line, col, error) {
  console.log("Глобальная ошибка поймана:", { msg, source, line, col });
  // Восстанавливаем старый обработчик
  setTimeout(() => {
    window.onerror = oldHandler;
  }, 1000);
  return false;
};

// Вызываем ошибку для теста
setTimeout(() => {
  nonexistentVariable.property; // Вызовет глобальную ошибку
}, 2000);
```

## 📝 Задания для закрепления

### Задание 1: Безопасное деление
Напиши функцию `safeDivide(a, b)`, которая делит `a` на `b`. Если `b` равно 0, выброси ошибку `Error("Деление на ноль")`. Оберни вызов функции в `try/catch` и выведи результат или сообщение об ошибке.

### Задание 2: Валидация возраста
Создай класс `ValidationError` (наследник `Error`) с дополнительным свойством `field`. Напиши функцию `validateAge(age)`, которая выбрасывает `ValidationError` если:
- `age` не число → `"age: должен быть числом"`
- `age` < 0 → `"age: не может быть отрицательным"`
- `age` > 150 → `"age: слишком большое значение"`

### Задание 3: Безопасный fetch
Напиши async-функцию `safeJsonFetch(url)`, которая:
1. Загружает данные по URL через `fetch`
2. Парсит ответ как JSON
3. При **любой** ошибке (сеть, HTTP, парсинг) возвращает `null` вместо выброса исключения

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** Ошибки - это не враги, а помощники! Они показывают, что нужно исправить в коде. Используйте `try/catch` для рискованных операций, создайте информативные ошибки и всегда обрабатывайте асинхронные ошибки. 🛡️

Хорошая обработка ошибок делает код надежным и предсказуемым! 🎯

---

[⬅️ Предыдущая тема: Даты](dates-js.md) | [📚 Оглавление](README.md) | [Следующая тема: Регулярные выражения ➡️](regex-js.md)
