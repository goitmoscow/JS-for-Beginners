# JSON и работа с API 🌐

## 🎦 Что такое JSON?

Представь JSON как **универсальный язык общения**:

🗣️ **Человек** = JavaScript object  
📝 **JSON** = текстовое представление объекта  
🌐 **Разные системы** = понимают этот язык

```javascript
// JavaScript object
const user = {
  name: "Анна",
  возраст: 25,
  город: "Москва",
};

// JSON представление
const jsonUser = '{"name":"Анна","возраст":25,"город":"Москва"}';
```

## 🔄 JSON.stringify() - преобразование в JSON

### 🎯 Базовое использование

```javascript
const user = {
  name: "Иван",
  возраст: 30,
  онлайн: true,
  хобби: ["программирование", "музыка", "спорт"],
};

const json = JSON.stringify(user);
console.log(json);
// {"name":"Иван","возраст":30,"онлайн":true,"хобби":["программирование","музыка","спорт"]}
```

### 🎯 Красивое форматирование

```javascript
const data = {
  users: [
    { name: "Анна", возраст: 25 },
    { name: "Борис", возраст: 30 },
  ],
  версия: "1.0",
  создан: new Date(),
};

const prettyJson = JSON.stringify(data, null, 2);
console.log(prettyJson);

/*
{
  "users": [
    {
      "name": "Анна",
      "возраст": 25
    },
    {
      "name": "Борис",
      "возраст": 30
    }
  ],
  "версия": "1.0",
  "создан": "2023-10-25T15:30:45.123Z"
}
*/
```

### 🎯 Фильтрация свойств

```javascript
const user = {
  id: 123,
  name: "Анна",
  email: "anna@example.com",
  пароль: "secret123",
  администратор: false,
  создан: new Date(),
};

// Функция-фильтр
const jsonWithoutPassword = JSON.stringify(
  user,
  (key, value) => {
    // Исключаем пароль
    if (key === "пароль") return undefined;

    // Date.toJSON уже превратил дату в ISO-строку до вызова replacer.

    return value;
  },
  2,
);

console.log(jsonWithoutPassword);
```

Date.toJSON вызывается перед replacer: функция получает уже строку даты. JSON поддерживает не только объекты, но и массивы, строки, числа, boolean и null. BigInt и циклические ссылки по умолчанию вызывают TypeError; NaN и Infinity сериализуются как null. undefined в объекте пропускается, а в массиве заменяется null.

### 🎯 Ограничения JSON

```javascript
const complexObject = {
  функция: () => console.log("привет"), // ❌ Не сериализуется
  символ: Symbol("id"), // ❌ Не сериализуется
  undefined_свойство: undefined, // ❌ Исключается
  пусто: null, // ✅ Сериализуется
  дата: new Date(), // ✅ Превращается в строку
  regexp: /тест/gi, // ✅ Превращается в {}
};

const json = JSON.stringify(complexObject, null, 2);
console.log(json);

/*
{
  "пусто": null,
  "дата": "2023-10-25T15:30:45.123Z",
  "regexp": {}
}
*/
```

## 🔄 JSON.parse() - преобразование из JSON

### 🎯 Базовое использование

```javascript
const jsonString = '{"name":"Мария","возраст":28,"город":"Санкт-Петербург"}';

const object = JSON.parse(jsonString);
console.log(object);
// { name: "Мария", возраст: 28, город: "Санкт-Петербург" }

console.log(object.name); // "Мария"
```

### 🎯 Обработка ошибок парсинга

```javascript
const invalidJson = '{"name":"Анна","возраст":25'; // Пропущена закрывающая скобка

function safeParse(json) {
  try {
    return JSON.parse(json);
  } catch (error) {
    console.error("Ошибка парсинга JSON:", error.message);
    return null;
  }
}

const parseResult = safeParse(invalidJson);
console.log(parseResult); // null
```

### 🎯 Восстановление дат

```javascript
const jsonWithDate =
  '{"name":"Пользователь","создан":"2023-10-25T15:30:45.123Z"}';

function parseWithDates(json) {
  return JSON.parse(json, (key, value) => {
    // Восстанавливаем даты
    if (key === "создан" && typeof value === "string" && /^\d{4}-\d{2}-\d{2}T/.test(value)) {
      return new Date(value);
    }
    return value;
  });
}

const restored = parseWithDates(jsonWithDate);
console.log(restored);
// { name: "Пользователь", создан: Date }
console.log(restored.создан instanceof Date); // true
```

## 🌐 Fetch API - работа с сервером

### 🎯 GET запрос

```javascript
async function getUsers() {
  try {
    console.log("Загружаем пользователей...");

    const response = await fetch("https://jsonplaceholder.typicode.com/users");

    if (!response.ok) {
      throw new Error(`HTTP ошибка: ${response.status}`);
    }

    const users = await response.json();
    console.log("Пользователи загружены:", users);

    return users;
  } catch (error) {
    console.error("Ошибка загрузки:", error.message);
    return [];
  }
}

// Использование
getUsers().then((users) => {
  console.log(`Загружено ${users.length} пользователей`);
  users.slice(0, 3).forEach((user) => {
    console.log(`- ${user.name} (${user.email})`);
  });
});
```

### 🎯 POST запрос с JSON

```javascript
async function createUser(userData) {
  try {
    console.log("Создаем пользователя:", userData);

    const response = await fetch("https://jsonplaceholder.typicode.com/users", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
      },
      body: JSON.stringify(userData),
    });

    if (!response.ok) {
      throw new Error(`Не удалось создать пользователя: ${response.status}`);
    }

    const created = await response.json();
    console.log("Пользователь создан:", created);

    return created;
  } catch (ошибка) {
    console.error("Ошибка создания:", ошибка.message);
    return null;
  }
}

// Использование
const newUser = {
  name: "Анна Петрова",
  email: "anna.petrova@example.com",
  phone: "+7(999)123-45-67",
  website: "annapetrova.com",
};

createUser(newUser);
```

### 🎯 PUT запрос (обновление)

```javascript
async function updateUser(id, data) {
  try {
    console.log(`Обновляем пользователя ${id}:`, data);

    const response = await fetch(
      `https://jsonplaceholder.typicode.com/users/${id}`,
      {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      },
    );

    if (!response.ok) {
      throw new Error(`Не удалось обновить: ${response.status}`);
    }

    const updated = await response.json();
    console.log("Пользователь обновлен:", updated);

    return updated;
  } catch (ошибка) {
    console.error("Ошибка обновления:", ошибка.message);
    return null;
  }
}

// Использование
updateUser(1, {
  name: "Обновленный user",
  email: "updated@example.com",
  phone: "+7(888)987-65-43",
});
```

### 🎯 DELETE запрос

```javascript
async function deleteUser(id) {
  try {
    console.log(`Удаляем пользователя ${id}...`);

    const response = await fetch(
      `https://jsonplaceholder.typicode.com/users/${id}`,
      {
        method: "DELETE",
      },
    );

    if (!response.ok) {
      throw new Error(`Не удалось удалить: ${response.status}`);
    }

    console.log(`Пользователь ${id} удален`);
    return true;
  } catch (ошибка) {
    console.error("Ошибка удаления:", ошибка.message);
    return false;
  }
}

// Использование
deleteUser(1);
```

Относительные URL /api/... требуют вашего сервера. JSONPlaceholder имитирует запись данных и не хранит ваши изменения. fetch не считает HTTP 404/500 сетевой ошибкой: перед response.json() проверяйте response.ok.

## 💾 LocalStorage и SessionStorage

Используйте отдельную учебную страницу. Хранилище относится к origin сайта; пример не должен очищать чужие ключи. Данные из хранилища нужно не только разобрать как JSON, но и проверить по ожидаемой структуре.

### 🎯 LocalStorage - хранилище браузера

```javascript
// Сохранение данных
const user = {
  id: 123,
  name: "Анна",
  настройки: {
    тема: "темная",
    язык: "ru",
  },
};

// Сохраняем как JSON строку
localStorage.setItem("user", JSON.stringify(user));

// Получение данных
const saved = localStorage.getItem("user");
if (saved) {
  const restored = JSON.parse(saved);
  console.log("Восстановленный пользователь:", restored);
}

// Проверка наличия данных
function getUser() {
  const data = localStorage.getItem("user");
  return data ? JSON.parse(data) : null;
}

// Удаление данных
localStorage.removeItem("user");

// localStorage.clear() очищает всё хранилище этого сайта.
// Для учебного примера удаляйте только собственный ключ через removeItem.
```

### 🎯 SessionStorage - временное хранилище

```javascript
// Работает так же, как localStorage, но очищается при закрытии вкладки
sessionStorage.setItem(
  "временные_данные",
  JSON.stringify({
    время_входа: new Date(),
    просмотры: 0,
  }),
);

// Увеличиваем счетчик просмотров
function increaseViews() {
  const data = sessionStorage.getItem("временные_данные");
  if (data) {
    let temporary = JSON.parse(data);
    temporary.просмотры++;
    sessionStorage.setItem("временные_данные", JSON.stringify(temporary));
    console.log(`Просмотров: ${temporary.просмотры}`);
  }
}

// Вызываем при каждой загрузке страницы
increaseViews();
```

### 🎯 Работа с хранилищем через класс

```javascript
class Хранилище {
  constructor(key) {
    this.key = key;
  }

  сохранить(data) {
    try {
      localStorage.setItem(this.key, JSON.stringify(data));
      return true;
    } catch (ошибка) {
      console.error("Ошибка сохранения:", ошибка.message);
      return false;
    }
  }

  загрузить() {
    try {
      const data = localStorage.getItem(this.key);
      return data ? JSON.parse(data) : null;
    } catch (ошибка) {
      console.error("Ошибка загрузки:", ошибка.message);
      return null;
    }
  }

  удалить() {
    localStorage.removeItem(this.key);
  }

  существует() {
    return localStorage.getItem(this.key) !== null;
  }
}

// Использование
const settingsStorage = new Хранилище("настройки_пользователя");

const settings = {
  тема: "светлая",
  язык: "ru",
  уведомления: true,
};

settingsStorage.сохранить(settings);

const loaded = settingsStorage.загрузить();
console.log("Настройки:", loaded);
```

## 🌐 Практические примеры

### 🛒 Корзина покупок с localStorage

```javascript
class Cart {
  constructor() {
    this.key = "cart_items";
    this.items = this.load() || [];
  }

  load() {
    try {
      const data = localStorage.getItem(this.key);
      const parsed = data ? JSON.parse(data) : [];
      return Array.isArray(parsed) ? parsed : [];
    } catch (error) {
      console.error("Ошибка загрузки корзины:", error);
      return [];
    }
  }

  save() {
    try {
      localStorage.setItem(this.key, JSON.stringify(this.items));
    } catch (error) {
      console.error("Ошибка сохранения корзины:", error);
    }
  }

  add(item) {
    const quantity = item.quantity ?? 1;
    if (!Number.isInteger(quantity) || quantity <= 0) throw new RangeError("Количество должно быть положительным целым");
    const existing = this.items.find((i) => i.id === item.id);

    if (existing) {
      existing.quantity += quantity;
    } else {
      this.items.push({
        ...item,
        quantity,
        added: new Date().toISOString(),
      });
    }

    this.save();
    console.log(`Товар добавлен: ${item.name}`);
  }

  remove(id) {
    this.items = this.items.filter((i) => i.id !== id);
    this.save();
    console.log(`Товар ${id} удален из корзины`);
  }

  clear() {
    this.items = [];
    this.save();
    console.log("Корзина очищена");
  }

  getTotal() {
    return this.items.reduce((total, item) => {
      return total + item.price * item.quantity;
    }, 0);
  }

  getCount() {
    return this.items.reduce((sum, item) => sum + item.quantity, 0);
  }
}

// Использование
const cart = new Cart();

cart.add({
  id: 1,
  name: "Ноутбук",
  price: 50000,
  quantity: 1,
});

cart.add({
  id: 2,
  name: "Мышь",
  price: 1500,
  quantity: 2,
});

console.log("Товаров в корзине:", cart.getCount());
console.log("Общая сумма:", cart.getTotal());
```

### 🌐 API клиент

```javascript
class APIClient {
  constructor(baseUrl) {
    this.baseUrl = baseUrl;
    this.token = localStorage.getItem("auth_token");
  }

  async request(path, options = {}) {
    const url = `${this.baseUrl}${path}`;

    const headers = new Headers(options.headers);
    if (!headers.has("Content-Type")) headers.set("Content-Type", "application/json");
    if (this.token) headers.set("Authorization", `Bearer ${this.token}`);
    const settings = { ...options, headers };

    try {
      const response = await fetch(url, settings);

      if (!response.ok) {
        if (response.status === 401) {
          // Токен просрочен, удаляем его
          this.logout();
          throw new Error("Требуется авторизация");
        }
        throw new Error(`HTTP ${response.status}: ${response.statusText}`);
      }

      if (response.status === 204) return null;
      const data = await response.json();
      return data;
    } catch (error) {
      console.error(`Ошибка запроса к ${url}:`, error.message);
      throw error;
    }
  }

  async get(path) {
    return this.request(path);
  }

  async post(path, data) {
    return this.request(path, {
      method: "POST",
      body: JSON.stringify(data),
    });
  }

  async put(path, data) {
    return this.request(path, {
      method: "PUT",
      body: JSON.stringify(data),
    });
  }

  async delete(path) {
    return this.request(path, {
      method: "DELETE",
    });
  }

  authorize(token) {
    this.token = token;
    localStorage.setItem("auth_token", token);
  }

  logout() {
    this.token = null;
    localStorage.removeItem("auth_token");
  }
}

// Использование
const api = new APIClient("https://jsonplaceholder.typicode.com");

// Получаем посты
api
  .get("/posts")
  .then((posts) => {
    console.log(`Загружено ${posts.length} постов`);
    return posts.slice(0, 3);
  })
  .then((первые_посты) => {
    console.log("Первые посты:", первые_посты);

    // Создаем новый пост
    return api.post("/posts", {
      title: "Новый пост",
      body: "Содержание нового поста",
      userId: 1,
    });
  })
  .then((created) => {
    console.log("Создан пост:", created);
  })
  .catch((ошибка) => {
    console.error("Ошибка работы с API:", ошибка.message);
  });
```

### 📊 Кэширование данных

```javascript
// APIClient определён в предыдущем примере.
class Cache {
  constructor(prefix = "js-beginners:cache:") {
    this.prefix = prefix;
    this.lifetime = 5 * 60 * 1000;
  }
  _key(key) { return this.prefix + key; }
  set(key, value) {
    localStorage.setItem(this._key(key), JSON.stringify({ value, time: Date.now() }));
  }
  get(key) {
    try {
      const raw = localStorage.getItem(this._key(key));
      if (raw === null) return null;
      const entry = JSON.parse(raw);
      if (!entry || !Number.isFinite(entry.time) || Date.now() - entry.time >= this.lifetime) {
        this.delete(key);
        return null;
      }
      return entry.value;
    } catch (error) {
      console.error("Не удалось прочитать кэш:", error.message);
      return null;
    }
  }
  delete(key) { localStorage.removeItem(this._key(key)); }
  clear() {
    const keys = Array.from({ length: localStorage.length }, (_, i) => localStorage.key(i));
    for (const key of keys) if (key.startsWith(this.prefix)) localStorage.removeItem(key);
  }
}
class CachedAPI extends APIClient {
  constructor(baseUrl) {
    super(baseUrl);
    this.cache = new Cache();
  }
  async getCached(path, useCache = true) {
    if (useCache) {
      const cached = this.cache.get(path);
      if (cached !== null) return cached; // Сохраняем 0, false и пустую строку
    }
    const data = await this.get(path);
    try { this.cache.set(path, data); }
    catch (error) { console.warn("Не удалось записать кэш:", error.message); }
    return data;
  }
}
async function cacheExample() {
  const api = new CachedAPI("https://jsonplaceholder.typicode.com");
  console.log(await api.getCached("/users/1")); // Первый запрос завершён
  console.log(await api.getCached("/users/1")); // Теперь можно использовать кэш
}
cacheExample().catch(console.error);
// В этом учебном API null означает отсутствие записи; данные предполагаются JSON-совместимыми.
```

## 🚨 Частые ошибки новичков

### ❌ Забытый JSON.stringify

```javascript
const user = { name: "Анна", возраст: 25 };

// ❌ ПЛОХО - сохраняем object напрямую (не будет работать!)
localStorage.setItem("user", user);

// ✅ ХОРОШО - преобразуем в JSON строку
localStorage.setItem("user", JSON.stringify(user));
```

### ❌ Забытый JSON.parse

```javascript
const json_строка = '{"name":"Анна","возраст":25}';

// ❌ ПЛОХО - пытаемся работать со строкой как с объектом
const name = json_строка.name; // undefined

// ✅ ХОРОШО - парсим JSON в object
const object = JSON.parse(json_строка);
const name2 = object.name; // "Анна"
```

### ❌ Обработка ошибок JSON

```javascript
const invalidJson = '{"name":"Анна"'; // Пропущена закрывающая скобка

// ❌ ПЛОХО - нет обработки ошибок
const data = JSON.parse(invalidJson); // Выбросит ошибку!

// ✅ ХОРОШО - обрабатываем ошибки
try {
  const data = JSON.parse(invalidJson);
} catch (ошибка) {
  console.error("Ошибка парсинга:", ошибка.message);
}
```

### ❌ Неправильные заголовки Fetch

```javascript
const data = { name: "Анна" };

// ❌ ПЛОХО - забыт заголовок Content-Type
fetch("/api/users", {
  method: "POST",
  body: JSON.stringify(data),
});

// ✅ ХОРОШО - правильный заголовок
fetch("/api/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
});
```

## 📚 Шпаргалка быстрых операций

| Задача                   | Метод                       | Пример                                              |
| ------------------------ | --------------------------- | --------------------------------------------------- |
| Преобразовать в JSON     | `JSON.stringify()`          | `JSON.stringify(obj, null, 2)`                      |
| Преобразовать из JSON    | `JSON.parse()`              | `JSON.parse(jsonString)`                            |
| GET запрос               | `fetch()`                   | `await fetch('/api/data')`                          |
| POST запрос              | `fetch()`                   | `await fetch('/api/data', {method: 'POST', ...})`   |
| Сохранить в localStorage | `localStorage.setItem()`    | `localStorage.setItem('key', JSON.stringify(data))` |
| Получить из localStorage | `localStorage.getItem()`    | `JSON.parse(localStorage.getItem('key'))`           |
| Удалить из localStorage  | `localStorage.removeItem()` | `localStorage.removeItem('key')`                    |
| Очистить localStorage    | `localStorage.clear()`      | `localStorage.clear()`                              |

## 🎮 Практика в консоли

Открой F12 на странице с HTTPS и попробуй:

```javascript
// 1. Работа с JSON
const user = { name: "Иван", возраст: 30 };
const json = JSON.stringify(user, null, 2);
console.log("JSON:", json);

const restored = JSON.parse(json);
console.log("Восстановленный:", restored);

// 2. Загрузка данных с API
async function getUsers() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    const users = await response.json();
    console.log("Пользователи:", users.slice(0, 3));

    // Сохраняем в localStorage
    localStorage.setItem("users", JSON.stringify(users));
    return users;
  } catch (error) {
    console.error("Ошибка:", error.message);
  }
}

getUsers();

// 3. Работа с localStorage
function saveSettings() {
  const settings = {
    тема: "темная",
    язык: "ru",
    уведомления: true,
    последняя_активность: new Date().toISOString(),
  };

  localStorage.setItem("настройки", JSON.stringify(settings));
  console.log("Настройки сохранены");
}

function loadSettings() {
  const saved = localStorage.getItem("настройки");
  if (saved) {
    const settings = JSON.parse(saved);
    console.log("Загруженные настройки:", settings);

    // Проверяем время последней активности
    const lastActivity = new Date(settings.последняя_активность);
    const now = new Date();
    const diff = now - lastActivity;
    const days = Math.floor(diff / (1000 * 60 * 60 * 24));

    console.log(`Прошло ${days} дней с последней активности`);
  } else {
    console.log("Настройки не найдены");
  }
}

// 4. Создание поста через API
async function createPost() {
  const post = {
    title: "Новый пост из консоли",
    body: "Это тестовый пост",
    userId: 1,
  };

  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(post),
    });

    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    const created = await response.json();
    console.log("Создан пост:", created);

    // Сохраняем ID созданного поста
    localStorage.setItem("lastPostId", created.id.toString());

    return created;
  } catch (ошибка) {
    console.error("Ошибка создания поста:", ошибка.message);
  }
}

// 5. Обработка ошибок парсинга
function safeJSONParse(jsonString) {
  try {
    return JSON.parse(jsonString);
  } catch (error) {
    console.error("Ошибка парсинга JSON:", error.message);
    return null;
  }
}

const goodJSON = '{"name":"Анна"}';
const badJSON = '{"name":"Анна"';

console.log("Хороший JSON:", safeJSONParse(goodJSON));
console.log("Плохой JSON:", safeJSONParse(badJSON));

// Вызываем все функции
saveSettings();
loadSettings();
createPost();
```

## 📝 Задания для закрепления

### Задание 1: JSON туда и обратно
Создай объект пользователя с полями `name`, `age`, `hobbies` (массив). Преобразуй его в JSON-строку с красивым форматированием (отступ 2 пробела), затем восстанови обратно в объект и выведи значение `hobbies[0]`.

### Задание 2: Безопасное хранилище
Напиши две функции:
- `saveData(key, data)` — сохраняет данные в localStorage (с JSON.stringify)
- `loadData(key)` — загружает данные из localStorage (с JSON.parse)
Обе функции должны обрабатывать ошибки через `try/catch` и возвращать `false`/`null` при ошибке.

### Задание 3: Пост с комментариями
Напиши async-функцию `getPostWithComments(postId)`, которая **параллельно** загружает пост и его комментарии с jsonplaceholder.typicode.com и возвращает объект `{ post, comments }`.
```javascript
// URL поста: https://jsonplaceholder.typicode.com/posts/{id}
// URL комментариев: https://jsonplaceholder.typicode.com/posts/{id}/comments
```

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** JSON - это универсальный формат для обмена данными между системами! Используй `JSON.stringify()` для отправки данных и `JSON.parse()` для получения. LocalStorage поможет сохранять data между сессиями. 🌐

Работа с API и JSON - это как общение на разных языках через переводчика! 🗣️📝

## Документация

- [JSON.stringify — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
- [Использование Fetch — MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)


---

[⬅️ Предыдущая тема: Регулярные выражения](regex-js.md) | [📚 Оглавление](README.md)
