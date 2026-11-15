# Асинхронный JavaScript ⏳

## 🎦 Что такое асинхронность?

Представь асинхронность как **заказ пиццы**:

📞 **Звонок в пиццерию** = отправляем запрос  
⏰ **Ждем приготовления** = асинхронная операция  
🍕 **Получаем пиццу** = результат приходит позже  
☕ **Тем временем пьем кофе** = программа продолжает работать

```javascript
// Синхронно (по очереди)
console.log("1");
console.log("2");
console.log("3"); // 1, 2, 3

// Асинхронно (некоторые операции занимают время)
console.log("1");
setTimeout(() => console.log("2"), 1000); // через 1 секунду
console.log("3"); // 1, 3, 2
```

## ⏳ Колбэки (Callbacks)

Callback — функция, переданная другому коду для вызова. Она бывает синхронной, как в map, или вызывается позже, как в setTimeout. Промисы и async/await помогают организовать асинхронные операции, но не заменяют все колбэки.

### 🎯 Базовый колбэк

```javascript
function makeCoffee(callback) {
  console.log("Варим кофе...");
  setTimeout(() => {
    console.log("Кофе готов!");
    callback("Кофе доставлен");
  }, 2000);
}

makeCoffee(function (сообщение) {
  console.log(сообщение);
  console.log("Можно пить!");
});

// Вывод:
// Варим кофе...
// (через 2 секунды)
// Кофе готов!
// Кофе доставлен
// Можно пить!
```

### 🎯 Колбэки с ошибками

```javascript
function loadUser(id, callback) {
  console.log(`Загружаем пользователя ${id}...`);

  // Симуляция загрузки (может быть ошибка)
  setTimeout(() => {
    if (id > 0) {
      callback(null, { id, имя: `Пользователь${id}` });
    } else {
      callback(new Error("Некорректный ID пользователя"));
    }
  }, 1000);
}

loadUser(1, (error, user) => {
  if (error) {
    console.error("Ошибка:", error.message);
    return;
  }

  console.log("Загружен:", user);
});
```

### 🎯 Проблема "Callback Hell"

```javascript
// ❌ ПЛОХО - вложенные колбэки
loadUser(1, (error, user) => {
  loadProfile(user.id, (error, profile) => {
    loadFriends(user.id, (error, friends) => {
      loadPhotos(user.id, (error, photos) => {
        console.log("Все данные загружены");
        // Глубоко и сложно читать!
      });
    });
  });
});
```

## 🎯 Промисы (Promises) - современный способ

### 🎦 Что такое промис?

Представь промис как **заказ на доставку**:

📦 **Заказ** = промис  
⏳ **В пути** = pending (ожидание)  
✅ **Доставлен** = fulfilled (выполнен)  
❌ **Проблема** = rejected (отклонен)

```javascript
const promise = new Promise((resolve, reject) => {
  // resolve - если все хорошо
  // reject - если что-то пошло не так

  setTimeout(() => {
    const success = Math.random() > 0.3; // 70% успеха

    if (success) {
      resolve("Операция выполнена успешно!");
    } else {
      reject(new Error("Что-то пошло не так"));
    }
  }, 1000);
});
```

### 🎯 then() и catch()

```javascript
promise
  .then((result) => {
    console.log("Успех:", result);
    return "Дополнительные данные";
  })
  .then((data) => {
    console.log("Дополнительные:", data);
  })
  .catch((error) => {
    console.error("Ошибка:", error.message);
  })
  .finally(() => {
    console.log("Операция завершена (в любом случае)");
  });
```

### 🎯 Промис-функции

```javascript
function loadData(url) {
  return new Promise((resolve, reject) => {
    console.log(`Загружаем данные с ${url}...`);

    setTimeout(() => {
      // Симуляция успешной загрузки
      if (url.includes("api")) {
        resolve({ data: "JSON с сервера", статус: 200 });
      } else {
        reject(new Error("Неверный URL"));
      }
    }, 1000);
  });
}

// Использование
loadData("https://api.example.com/users")
  .then((data) => {
    console.log("Получены данные:", data);
  })
  .catch((error) => {
    console.error("Ошибка загрузки:", error.message);
  });
```

### 🎯 Promise.all() - много промисов одновременно

```javascript
const promise1 = Promise.resolve("Первый результат");
const promise2 = new Promise((resolve) =>
  setTimeout(() => resolve("Второй результат"), 1000),
);
const promise3 = Promise.resolve("Третий результат");

Promise.all([promise1, promise2, promise3])
  .then((результаты) => {
    console.log("Все результаты:", результаты);
    // ["Первый результат", "Второй результат", "Третий результат"]
  })
  .catch((ошибка) => {
    console.error("Хотя бы один промис отклонен:", ошибка);
  });
```

### 🎯 Promise.race() - кто первый

```javascript
const fast = new Promise((resolve) =>
  setTimeout(() => resolve("Быстрый ответ"), 100),
);
const slow = new Promise((resolve) =>
  setTimeout(() => resolve("Медленный ответ"), 2000),
);

Promise.race([fast, slow]).then((winner) => {
  console.log("Первым пришел:", winner); // "Быстрый ответ"
});
```

## ⚡ async/await - самый современный способ

### 🎯 Базовый синтаксис

```javascript
async function getResult() {
  const result = await Promise.resolve("Готово");
  return result;
}
getResult().then(console.log);
// await допустим внутри async-функций, а также на верхнем уровне ES-модулей.

// async функции всегда возвращают промис
```

### 🎯 Пример с async/await

```javascript
async function fetchJson(url) {
  const response = await fetch(url);
  if (!response.ok) throw new Error(`HTTP ${response.status}`);
  return response.json();
}

async function loadUserWithPosts(id) {
  const user = await fetchJson(`https://jsonplaceholder.typicode.com/users/${id}`);
  const posts = await fetchJson(`https://jsonplaceholder.typicode.com/posts?userId=${id}`);
  return { user, posts };
}

loadUserWithPosts(1)
  .then((data) => console.log("Данные:", data))
  .catch((error) => console.error("Ошибка:", error.message));
```

### 🎯 Parallel async/await

```javascript
// В этом примере fetchJson — функция из предыдущего блока.
async function loadSequential(id) {
  const user = await fetchJson(`https://jsonplaceholder.typicode.com/users/${id}`);
  const posts = await fetchJson(`https://jsonplaceholder.typicode.com/posts?userId=${id}`);
  return { user, posts };
}

async function loadParallel(id) {
  const [user, posts] = await Promise.all([
    fetchJson(`https://jsonplaceholder.typicode.com/users/${id}`),
    fetchJson(`https://jsonplaceholder.typicode.com/posts?userId=${id}`),
  ]);
  return { user, posts };
}
// Параллельный вариант подходит для независимых запросов.
loadParallel(1).then(console.log).catch(console.error);
```

Promise.all сохраняет порядок входных промисов, но при первой ошибке отклоняется; уже начатые запросы не отменяются автоматически. Promise.race тоже не отменяет оставшиеся операции.

## 🌐 Fetch API - работа с сетью

fetch не отклоняет промис только из-за статуса HTTP 404 или 500. Проверяйте response.ok до чтения успешного результата. Примеры с /api/... предполагают ваш сервер; JSONPlaceholder — публичный учебный сервис, изменения в нём имитируются и не сохраняются.

### 🎯 Базовый GET запрос

```javascript
async function getUsers() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");

    if (!response.ok) {
      throw new Error(`HTTP ошибка: ${response.status}`);
    }

    const users = await response.json();
    console.log("Пользователи:", users);
    return users;
  }    catch (error) {
    console.error("Ошибка загрузки:", error.message);
  
  }
}

getUsers();
```

### 🎯 POST запрос с данными

```javascript
async function createUser(data) {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(data),
    });

    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    const created = await response.json();
    console.log("Создан пользователь:", created);
    return created;
  } catch (ошибка) {
    console.error("Ошибка создания:", ошибка.message);
  }
}

// Использование
createUser({
  имя: "Иван",
  email: "ivan@example.com",
  телефон: "+7-999-123-45-67",
});
```

### 🎯 PUT/PATCH запрос (обновление)

```javascript
async function updateUser(id, data) {
  try {
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

    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    const updated = await response.json();
    console.log("Обновлен пользователь:", updated);
    return updated;
  } catch (ошибка) {
    console.error("Ошибка обновления:", ошибка.message);
  }
}

updateUser(1, {
  имя: "Анна",
  email: "anna@example.com",
});
```

### 🎯 DELETE запрос

```javascript
async function deleteUser(id) {
  try {
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/users/${id}`,
      {
        method: "DELETE",
      },
    );

    if (response.ok) {
      console.log(`Пользователь ${id} удален`);
      return true;
    } else {
      throw new Error(`Не удалось удалить пользователя ${id}`);
    }
  } catch (ошибка) {
    console.error("Ошибка удаления:", ошибка.message);
  }
}

deleteUser(1);
```

## 🎯 Практические примеры

### 🎮 Асинхронная игра

```javascript
class AsyncGame {
  constructor() {
    this.score = 0;
    this.gameActive = false;
  }

  // Асинхронное генерирование вопроса
  async generateQuestion() {
    return new Promise((resolve) => {
      setTimeout(() => {
        const number1 = Math.floor(Math.random() * 10) + 1;
        const number2 = Math.floor(Math.random() * 10) + 1;
        const answer = number1 + number2;

        resolve({ question: `${number1} + ${number2} = ?`, answer });
      }, 1000);
    });
  }

  async start() {
    this.gameActive = true;
    console.log("🎮 Игра начата!");

    while (this.gameActive) {
      const { question, answer } = await this.generateQuestion();
      console.log(`❓ Вопрос: ${question}`);

      const userAnswer = await this.getAnswer(question);

      if (userAnswer === answer) {
        this.score++;
        console.log(`✅ Правильно! Счет: ${this.score}`);
      } else {
        console.log(`❌ Неправильно! Правильный ответ: ${answer}`);
        this.gameActive = false;
      }

      if (this.score >= 5) {
        console.log(`🎉 Победа! Финальный счет: ${this.score}`);
        this.gameActive = false;
      }
    }
  }

  getAnswer(question) {
    return new Promise((resolve) => {
      // В реальном приложении здесь был бы prompt или input
      setTimeout(() => {
        const answer = parseInt(prompt(question) || "0");
        resolve(answer);
      }, 100);
    });
  }
}

// Запуск игры
const game = new AsyncGame();
game.start().catch(console.error);
```

### 🛒 Асинхронная корзина покупок

```javascript
class Cart {
  constructor() {
    this.products = [];
  }

  // Асинхронное добавление товара
  async addProduct(id) {
    try {
      console.log(`Загружаем товар ${id}...`);

      const response = await fetch(
        `https://jsonplaceholder.typicode.com/posts/${id}`,
      );
      if (!response.ok) throw new Error(`HTTP ${response.status}`);
      const product = await response.json();

      product.quantity = 1;
      product.price = Math.floor(Math.random() * 1000) + 100;

      // Проверяем, есть ли уже такой товар
      const existing = this.products.find((t) => t.id === id);
      if (existing) {
        existing.quantity++;
      } else {
        this.products.push(product);
      }

      console.log(`✅ Товар добавлен: ${product.title.substring(0, 30)}...`);
      this.showCart();

      return product;
    } catch (error) {
      console.error(`❌ Ошибка добавления товара ${id}:`, error.message);
    }
  }

  // Асинхронное оформление заказа
  async placeOrder() {
    if (this.products.length === 0) {
      console.log("❌ Корзина пуста!");
      return;
    }

    console.log("🛒 Оформляем заказ...");

    // Симуляция отправки заказа на сервер
    return new Promise((resolve) => {
      setTimeout(() => {
        const order = {
          id: Date.now(),
          products: [...this.products],
          total: this.calculateTotal(),
          date: new Date().toISOString(),
        };

        this.products = [];
        console.log("✅ Заказ оформлен:", order);
        resolve(order);
      }, 2000);
    });
  }

  showCart() {
    console.log("🛍️ Текущая корзина:");
    this.products.forEach((product, index) => {
      console.log(
        `${index + 1}. ${product.title.substring(0, 30)}... (${product.quantity} шт.)`,
      );
    });
    console.log(`💰 Итого: ${this.calculateTotal()} руб.`);
  }

  calculateTotal() {
    return this.products.reduce(
      (sum, product) => sum + product.price * product.quantity,
      0,
    );
  }
}

// Использование
async function cartExample() {
  const cart = new Cart();

  await cart.addProduct(1);
  await cart.addProduct(3);
  await cart.addProduct(1); // Добавим еще первого товара

  await cart.placeOrder();
}

cartExample();
```

### 🎵 Асинхронный аудиоплеер

```javascript
class AudioPlayer {
  constructor() {
    this.queue = [];
    this.current = null;
    this.isPlaying = false;
  }

  // Асинхронная загрузка трека
  async loadTrack(url) {
    return new Promise((resolve, reject) => {
      console.log(`📥 Загружаем трек: ${url}`);

      // Симуляция загрузки аудио
      setTimeout(() => {
        if (Math.random() > 0.2) {
          // 80% успеха
          resolve({
            url,
            title: `Трек ${url.split("/").pop()}`,
            duration: Math.floor(Math.random() * 200) + 120,
          });
        } else {
          reject(new Error(`Не удалось загрузить трек: ${url}`));
        }
      }, 1500);
    });
  }

  // Асинхронное добавление в очередь
  async addToQueue(url) {
    try {
      const track = await this.loadTrack(url);
      this.queue.push(track);
      console.log(`✅ Добавлен в очередь: ${track.title}`);
      this.showQueue();
    } catch (error) {
      console.error(`❌ Ошибка загрузки:`, error.message);
    }
  }

  // Асинхронное воспроизведение
  async play() {
    if (this.queue.length === 0) {
      console.log("❌ Очередь пуста!");
      return;
    }

    if (this.isPlaying) {
      console.log("⏸️ Уже играет!");
      return;
    }

    this.isPlaying = true;

    while (this.queue.length > 0 && this.isPlaying) {
      this.current = this.queue.shift();

      console.log(`▶️ Играет: ${this.current.title}`);

      // Воспроизведение (асинхронное ожидание)
      await this.playTrack(this.current);
    }

    this.isPlaying = false;
    console.log("🔇 Воспроизведение завершено");
  }

  playTrack(track) {
    return new Promise((resolve) => {
      console.log(`⏱️ Длительность: ${track.duration} сек`);

      setTimeout(() => {
        console.log(`✅ Завершен: ${track.title}`);
        resolve();
      }, track.duration * 1000);
    });
  }

  pause() {
    this.isPlaying = false;
    console.log("⏸️ Пауза");
  }

  showQueue() {
    console.log("📋 Очередь воспроизведения:");
    this.queue.forEach((track, index) => {
      console.log(`${index + 1}. ${track.title} (${track.duration} сек)`);
    });
  }
}

// Использование
async function playerExample() {
  const player = new AudioPlayer();

  await player.addToQueue("/music/track1.mp3");
  await player.addToQueue("/music/track2.mp3");
  await player.addToQueue("/music/track3.mp3");

  console.log("🎵 Начинаем воспроизведение...");
  await player.play();
}

// playerExample();
```

## 🚨 Частые ошибки новичков

### ❌ Забытый await

```javascript
async function getData() {
    // ❌ ПЛОХО - не ждем результата
    const data = fetch('/api/data');
    console.log(data); // Promise объект, а не данные!

    // ✅ ХОРОШО - ждем результат
    const correctData = await fetch('/api/data');
    const json = await correctData.json();
    console.log(json); // Настоящие данные!
}
```

### ❌ Неправильная обработка ошибок

```javascript
async function loadData() {
  try {
    // Все операции, которые здесь await-ятся, попадают в этот catch.
    const response = await fetch("https://jsonplaceholder.typicode.com/users/1");
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    return await response.json(); // await нужен для обработки ошибки чтения здесь
  } catch (error) {
    console.error("Ошибка:", error.message);
    return null;
  }
}
// Без await или return промис нужно обрабатывать отдельно через .catch().
```

### ❌ Смешивание колбэков и промисов

```javascript
// ❌ ПЛОХО - путаница стилей
fetch("/api/data").then((response) => {
  response.json((data) => {
    // ❌ response.json() возвращает промис!
    console.log(data);
  });
});

// ✅ ХОРОШО - последовательные then
fetch("/api/data")
  .then((response) => response.json())
  .then((data) => console.log(data));

// ✅ ИЛИ с async/await
async function loadData() {
  const response = await fetch("/api/data");
  const data = await response.json();
  console.log(data);
}
```

### ❌ Забытый return в then

```javascript
// ❌ ПЛОХО - цепочка прерывается
fetch("/api/user")
  .then((response) => {
    response.json(); // ❌ Забыт return!
  })
  .then((data) => {
    console.log(data); // undefined
  });

// ✅ ХОРОШО - возвращаем результат
fetch("/api/user")
  .then((response) => {
    return response.json(); // ✅ Явный return
  })
  .then((data) => {
    console.log(data); // Данные пользователя
  });
```

## 📚 Шпаргалка асинхронности

| Метод                  | Когда использовать        | Пример                               |
| ---------------------- | ------------------------- | ------------------------------------ |
| **Callback**           | Старый код, совместимость | `fs.readFile(path, callback)`        |
| **Promise**            | Современный код, цепочки  | `fetch().then().catch()`             |
| **async/await**        | Самый читаемый код        | `const data = await fetch()`         |
| **Promise.all**        | Параллельные операции     | `await Promise.all([p1, p2])`        |
| **Promise.race**       | Кто первый выполнится     | `await Promise.race([p1, p2])`       |
| **Promise.allSettled** | Ждем все операции         | `await Promise.allSettled([p1, p2])` |

## 🎮 Практика в консоли

Открой F12 и попробуй:

```javascript
// 1. Простой промис
const myPromise = new Promise((resolve) => {
  setTimeout(() => resolve("Привет из промиса!"), 2000);
});

myPromise.then((result) => console.log(result));

// 2. Асинхронная функция
async function test() {
  console.log("Начинаем...");
  await new Promise((resolve) => setTimeout(resolve, 1000));
  console.log("Прошла секунда!");
  await new Promise((resolve) => setTimeout(resolve, 1000));
  console.log("Прошло две секунды!");
}

test();

// 3. Fetch запрос (работает на страницах с HTTPS)
async function loadData() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
    const data = await response.json();
    console.log("Загружены данные:", data);
  } catch (ошибка) {
    console.error("Ошибка:", ошибка.message);
  }
}

loadData();

// 4. Параллельные запросы
async function parallel() {
  const [user, посты] = await Promise.all([
    fetch("https://jsonplaceholder.typicode.com/users/1").then((r) => r.json()),
    fetch("https://jsonplaceholder.typicode.com/posts?userId=1").then((r) =>
      r.json(),
    ),
  ]);

  console.log("Пользователь:", user);
  console.log("Посты:", посты.slice(0, 3)); // Первые 3 поста
}

parallel();

// 5. Обработка ошибок
async function withError() {
  try {
    const response = await fetch(
      "https://jsonplaceholder.typicode.com/users/999999",
    );
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }
    const data = await response.json();
  } catch (ошибка) {
    console.error("Поймана ошибка:", ошибка.message);
  }
}

withError();
```

## 📝 Задания для закрепления

### Задание 1: Функция delay
Создай функцию `delay(ms)`, возвращающую промис, который разрешается через `ms` миллисекунд. Используй её в async-функции для последовательного вывода:
- "Старт" → (пауза 1 сек) → "Середина" → (пауза 1 сек) → "Конец"

### Задание 2: Загрузка пользователя
Напиши async-функцию `fetchUserInfo(id)`, которая загружает пользователя с `https://jsonplaceholder.typicode.com/users/{id}` и возвращает объект только с полями `{name, email, city}`. Город находится в `user.address.city`. Обработай ошибки.

### Задание 3: Параллельная загрузка
Напиши функцию `loadAllUsers(ids)`, которая принимает массив ID пользователей и загружает всех параллельно с помощью `Promise.all`. Верни массив объектов `{name, email}`.
```javascript
loadAllUsers([1, 2, 3]).then(users => console.log(users));
// [{ name: "Leanne Graham", email: "..." }, ...]
```

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** Асинхронность позволяет JavaScript не блокировать интерфейс во время долгих операций! Используй `async/await` для читаемости и `try/catch` для обработки ошибок. ⏳

Асинхронный код - это как многозадачность в реальной жизни: можно пить кофе, пока пицца готовится! 🍕☕

## Документация

- [async function — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- [Использование Fetch — MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)


---

[⬅️ Предыдущая тема: Функции (продвинутые)](advanced-functions.md) | [📚 Оглавление](README.md) | [Следующая тема: DOM-манипуляции ➡️](dom-manipulation.md)
