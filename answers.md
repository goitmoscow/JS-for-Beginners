# Ответы к заданиям

> **Важно:** Сначала попробуй решить задание самостоятельно! Заглядывай сюда только для проверки или если совсем застрял.

---

## Что такое JavaScript (`what-is-js.md`)

### Задание 1: Первый alert

```javascript
alert("Иван"); // Замени на своё имя
```

### Задание 2: Первый console.log

```javascript
console.log("Привет, мир!");
```

---

## Переменные и константы (`variables-constants.md`)

### Задание 1: Профиль книги

```javascript
const title = "Война и мир";       // const — название не меняется
const author = "Лев Толстой";      // const — автор не меняется
const year = 1869;                  // const — год издания не меняется
const pages = 1225;                 // const — количество страниц не меняется
let isRead = false;                 // let — статус прочтения может измениться

isRead = true; // Прочитали книгу!
```

**Обоснование:** Характеристики книги (название, автор, год, страницы) неизменны — используем `const`. Статус прочтения может меняться — используем `let`.

### Задание 2: Предскажи результат

```javascript
const fruits = ["apple", "banana"];
fruits.push("orange");
console.log(fruits.length); // 3 — push добавляет элемент, массив можно мутировать через const

fruits = ["grape"]; // TypeError: Assignment to constant variable.
// const защищает от переприсвоения, но НЕ от изменения содержимого
```

### Задание 3: Найди и исправь ошибки

```javascript
// Ошибка 1: имя переменной не может начинаться с цифры
let name1 = "Иван"; // Исправлено: 1name → name1

// Ошибка 2: нельзя переприсвоить const
let age = 25; // Исправлено: const → let (если нужно менять)
age = 26;

// Ошибка 3: нельзя объявить переменную дважды с let
let x = 10;
x = 20; // Исправлено: убрали повторное let

// Ошибка 4: обращение до объявления (Temporal Dead Zone)
let userName = "Анна";
console.log(userName); // Исправлено: перенесли объявление ПЕРЕД использованием
```

### Задание 4: Игровые переменные

```javascript
const playerName = "Герой";
const maxHealth = 100;        // const — максимальное здоровье не меняется
let currentHealth = 100;      // let — текущее здоровье меняется
let level = 1;                // let — уровень растёт
let score = 0;                // let — очки накапливаются
let isAlive = true;           // let — статус может измениться

// Получение урона
currentHealth -= 20;
console.log("Здоровье:", currentHealth); // 80

// Набор очков
score += 50;
console.log("Очки:", score); // 50
```

---

## Типы данных (`types-js.md`)

### Задание 1: Определи тип

```javascript
typeof 42           // "number"
typeof "hello"      // "string"
typeof true         // "boolean"
typeof undefined    // "undefined"
typeof null         // "object"    ← историческая ошибка JS!
typeof [1, 2, 3]   // "object"    ← массив — это объект
typeof {}           // "object"
typeof function(){} // "function"
```

### Задание 2: Предскажи преобразование

```javascript
Number("123")    // 123
Number("abc")    // NaN
Number(true)     // 1
Number("")       // 0
String(42)       // "42"
Boolean(0)       // false
Boolean("false") // true  ← непустая строка всегда true!
Boolean("")      // false
```

### Задание 3: Хитрые сложения

```javascript
"5" + 3       // "53"  — строка + число = конкатенация
5 + "3"       // "53"  — число + строка = конкатенация
5 + 3 + "7"   // "87"  — сначала 5+3=8, потом 8+"7"="87"
"5" + 3 + 7   // "537" — сначала "5"+3="53", потом "53"+7="537"
"5" - 3       // 2     — минус ВСЕГДА преобразует в числа
true + true   // 2     — true = 1, поэтому 1 + 1 = 2
```

### Задание 4: Функция getType

```javascript
function getType(value) {
  if (value === null) return "null";
  if (Array.isArray(value)) return "array";
  return typeof value;
}

// Проверка:
console.log(getType(null));        // "null"
console.log(getType([1, 2]));      // "array"
console.log(getType(42));          // "number"
console.log(getType("hello"));    // "string"
console.log(getType({}));          // "object"
console.log(getType(undefined));   // "undefined"
```

---

## Операторы (`operators-js.md`)

### Задание 1: Вычисли результат

```javascript
let a = 10;
let b = 3;
console.log(a % b);     // 1       — остаток от деления 10/3
console.log(a ** 2);     // 100     — 10 в степени 2
console.log(++a + b--);  // 14      — сначала a=11 (++a), потом 11+3=14, потом b=2
console.log(a, b);       // 11 2    — a уже 11 после ++a, b стало 2 после b--
```

### Задание 2: Функция isEven

```javascript
function isEven(number) {
  return number % 2 === 0;
}

console.log(isEven(4));  // true
console.log(isEven(7));  // false
console.log(isEven(0));  // true
```

### Задание 3: Функция clamp

```javascript
function clamp(value, min, max) {
  if (value < min) return min;
  if (value > max) return max;
  return value;
}

console.log(clamp(5, 1, 10));  // 5
console.log(clamp(-3, 1, 10)); // 1
console.log(clamp(15, 1, 10)); // 10
```

### Задание 4: Калькулятор скидки

```javascript
function finalPrice(price, discount) {
  if (discount < 0 || discount > 100) return price;
  return price - (price * discount / 100);
}

console.log(finalPrice(1000, 20));  // 800
console.log(finalPrice(500, 50));   // 250
console.log(finalPrice(1000, 110)); // 1000 — некорректная скидка
console.log(finalPrice(1000, -5));  // 1000 — некорректная скидка
```

---

## Условия (`conditions-js.md`)

### Задание 1: Время года

```javascript
function getSeason(month) {
  if (month === 12 || month === 1 || month === 2) return "зима";
  if (month >= 3 && month <= 5) return "весна";
  if (month >= 6 && month <= 8) return "лето";
  if (month >= 9 && month <= 11) return "осень";
  return "неизвестный месяц";
}

console.log(getSeason(1));  // "зима"
console.log(getSeason(7));  // "лето"
console.log(getSeason(13)); // "неизвестный месяц"
```

### Задание 2: Цена билета

```javascript
function getTicketPrice(age, isStudent) {
  if (age < 12) return 0;
  if (isStudent) return 200;
  if (age >= 65) return 150;
  return 400;
}

console.log(getTicketPrice(8, false));   // 0
console.log(getTicketPrice(20, true));   // 200
console.log(getTicketPrice(70, false));  // 150
console.log(getTicketPrice(30, false));  // 400
```

### Задание 3: Тернарный оператор

```javascript
let temperature = 25;
let weather =
  temperature > 30 ? "жарко" :
  temperature > 20 ? "тепло" :
  temperature > 10 ? "прохладно" :
  "холодно";

console.log(weather); // "тепло"
```

### Задание 4: Калькулятор на switch

```javascript
function calc(a, operator, b) {
  switch (operator) {
    case "+": return a + b;
    case "-": return a - b;
    case "*": return a * b;
    case "/":
      if (b === 0) return "Ошибка: деление на ноль";
      return a / b;
    case "%":
      if (b === 0) return "Ошибка: деление на ноль";
      return a % b;
    default:
      return "Неизвестный оператор";
  }
}

console.log(calc(10, "+", 5));  // 15
console.log(calc(10, "/", 0));  // "Ошибка: деление на ноль"
console.log(calc(10, "^", 2)); // "Неизвестный оператор"
```

---

## Циклы (`loops-js.md`)

### Задание 1: FizzBuzz

```javascript
for (let i = 1; i <= 30; i++) {
  if (i % 3 === 0 && i % 5 === 0) {
    console.log("FizzBuzz");
  } else if (i % 3 === 0) {
    console.log("Fizz");
  } else if (i % 5 === 0) {
    console.log("Buzz");
  } else {
    console.log(i);
  }
}
```

### Задание 2: Переворот строки

```javascript
function reverseString(str) {
  let result = "";
  for (let i = str.length - 1; i >= 0; i--) {
    result += str[i];
  }
  return result;
}

console.log(reverseString("hello"));      // "olleh"
console.log(reverseString("JavaScript")); // "tpircSavaJ"
```

### Задание 3: Пирамида

```javascript
function pyramid(n) {
  for (let i = 1; i <= n; i++) {
    console.log("*".repeat(i));
  }
}

pyramid(5);
// *
// **
// ***
// ****
// *****
```

### Задание 4: Поиск дубликатов

```javascript
function findDuplicates(array) {
  const duplicates = [];
  for (let i = 0; i < array.length; i++) {
    // Если элемент встречается ещё раз после текущей позиции
    // и ещё не добавлен в результат
    if (array.indexOf(array[i]) !== i && !duplicates.includes(array[i])) {
      duplicates.push(array[i]);
    }
  }
  return duplicates;
}

console.log(findDuplicates([1, 2, 3, 2, 4, 3, 5])); // [2, 3]
```

---

## Функции (`function.md`)

### Задание 1: Определи порядок вывода

```javascript
console.log("A");          // 1. Выведет "A"

function greet() {
  console.log("B");
  return "C";
}

console.log("D");          // 2. Выведет "D" (функция объявлена, но не вызвана)
const result = greet();    // 3. Вызов функции — выведет "B"
console.log(result);       // 4. Выведет "C" (возвращённое значение)
console.log("E");          // 5. Выведет "E"

// Итого: A, D, B, C, E
```

### Задание 2: Создай и вызови

```javascript
function multiply(a, b) {
  return a * b;
}

const result = multiply(7, 8);
console.log(result); // 56
```

### Задание 3: Ссылка vs вызов

```javascript
function greet() {
  return "Привет!";
}

console.log(greet);   // [Function: greet] — ссылка на функцию (сам объект функции)
console.log(greet()); // "Привет!" — вызов функции (результат выполнения)
```

**Пояснение:** `greet` без скобок — это ссылка на функцию как значение. `greet()` со скобками — это вызов функции, возвращающий результат.

---

## Строки (`strings-js.md`)

### Задание 1: Заглавные буквы

```javascript
function capitalize(str) {
  return str
    .split(" ")
    .map(word => word.charAt(0).toUpperCase() + word.slice(1))
    .join(" ");
}

console.log(capitalize("привет мир"));          // "Привет Мир"
console.log(capitalize("javascript для всех")); // "Javascript Для Всех"
```

### Задание 2: Палиндром

```javascript
function isPalindrome(str) {
  const clean = str.toLowerCase().replace(/\s/g, "");
  const reversed = clean.split("").reverse().join("");
  return clean === reversed;
}

console.log(isPalindrome("шалаш"));                       // true
console.log(isPalindrome("Анна"));                        // true
console.log(isPalindrome("привет"));                      // false
console.log(isPalindrome("А роза упала на лапу Азора"));  // true
```

### Задание 3: Обрезка строки

```javascript
function truncate(str, maxLength) {
  if (str.length <= maxLength) return str;
  return str.slice(0, maxLength) + "...";
}

console.log(truncate("Привет мир!", 7));  // "Привет ..."
console.log(truncate("Привет", 10));      // "Привет"
```

### Задание 4: Подсчёт гласных

```javascript
function countVowels(str) {
  const vowels = "аеёиоуыэюяАЕЁИОУЫЭЮЯ";
  let count = 0;
  for (const char of str) {
    if (vowels.includes(char)) count++;
  }
  return count;
}

console.log(countVowels("Привет мир")); // 3 (и, е, и)
console.log(countVowels("JavaScript")); // 3 (a, a, i) — английские не считаем!
```

> **Примечание:** Если нужно считать и английские гласные, добавь их в строку `vowels`.

---

## Массивы (`arrays-js.md`)

### Задание 1: Уникальные элементы

```javascript
function unique(array) {
  const result = [];
  for (const item of array) {
    if (!result.includes(item)) {
      result.push(item);
    }
  }
  return result;
}

// Или короткий способ через Set:
// const unique = (array) => [...new Set(array)];

console.log(unique([1, 2, 2, 3, 3, 3, 4])); // [1, 2, 3, 4]
console.log(unique(["a", "b", "a", "c"]));   // ["a", "b", "c"]
```

### Задание 2: Работа со студентами

```javascript
const students = [
  { name: "Анна", grade: 5 },
  { name: "Борис", grade: 3 },
  { name: "Виктор", grade: 4 },
  { name: "Галина", grade: 5 },
  { name: "Дмитрий", grade: 2 },
];

// 1. Средняя оценка
const average = students.reduce((sum, s) => sum + s.grade, 0) / students.length;
console.log("Средняя оценка:", average); // 3.8

// 2. Имена отличников
const excellent = students.filter(s => s.grade === 5).map(s => s.name);
console.log("Отличники:", excellent); // ["Анна", "Галина"]

// 3. Сортировка по оценке (от лучшей к худшей)
const sorted = [...students].sort((a, b) => b.grade - a.grade);
console.log(sorted);
// [{ name: "Анна", grade: 5 }, { name: "Галина", grade: 5 },
//  { name: "Виктор", grade: 4 }, { name: "Борис", grade: 3 },
//  { name: "Дмитрий", grade: 2 }]
```

### Задание 3: Разбить на группы

```javascript
function chunk(array, size) {
  const result = [];
  for (let i = 0; i < array.length; i += size) {
    result.push(array.slice(i, i + size));
  }
  return result;
}

console.log(chunk([1, 2, 3, 4, 5], 2));    // [[1, 2], [3, 4], [5]]
console.log(chunk([1, 2, 3, 4, 5, 6], 3)); // [[1, 2, 3], [4, 5, 6]]
```

### Задание 4: Плоский массив

```javascript
function flatten(array) {
  const result = [];
  for (const item of array) {
    if (Array.isArray(item)) {
      result.push(...flatten(item)); // Рекурсия для вложенных массивов
    } else {
      result.push(item);
    }
  }
  return result;
}

// Или встроенный способ:
// const flatten = (array) => array.flat(Infinity);

console.log(flatten([1, [2, [3, 4]], 5]));  // [1, 2, 3, 4, 5]
console.log(flatten([[1, 2], [3, [4]]]));   // [1, 2, 3, 4]
```

---

## Объекты (`objects-js.md`)

### Задание 1: Объект-автомобиль

```javascript
const car = {
  brand: "Toyota",
  model: "Camry",
  year: 2020,
  color: "синий",
  mileage: 45000,

  getInfo() {
    return `${this.brand} ${this.model} ${this.year}, цвет: ${this.color}, пробег: ${this.mileage} км`;
  }
};

console.log(car.getInfo());
// "Toyota Camry 2020, цвет: синий, пробег: 45000 км"
```

### Задание 2: Объединение объектов

```javascript
function mergeObjects(obj1, obj2) {
  return { ...obj1, ...obj2 };
}

console.log(mergeObjects({ a: 1, b: 2 }, { b: 3, c: 4 }));
// { a: 1, b: 3, c: 4 }
```

### Задание 3: Выбрать ключи

```javascript
function pick(obj, keys) {
  const result = {};
  for (const key of keys) {
    if (key in obj) {
      result[key] = obj[key];
    }
  }
  return result;
}

const user = { name: "Анна", age: 25, email: "a@b.com", city: "Москва" };
console.log(pick(user, ["name", "email"]));
// { name: "Анна", email: "a@b.com" }
```

---

## Продвинутые функции (`advanced-functions.md`)

### Задание 1: Стрелочные функции

```javascript
const double = x => x * 2;
const isPositive = x => x > 0;
const getFullName = (first, last) => first + " " + last;

console.log(double(5));              // 10
console.log(isPositive(-3));         // false
console.log(getFullName("Иван", "Петров")); // "Иван Петров"
```

### Задание 2: Счётчик на замыкании

```javascript
function createCounter(start) {
  let value = start;

  return {
    increment() { value++; },
    decrement() { value--; },
    getValue() { return value; }
  };
}

const counter = createCounter(10);
counter.increment();   // 11
counter.increment();   // 12
counter.decrement();   // 11
console.log(counter.getValue()); // 11
```

### Задание 3: Функция once

```javascript
function once(fn) {
  let called = false;
  let result;

  return function (...args) {
    if (!called) {
      called = true;
      result = fn(...args);
    }
    return result;
  };
}

const initialize = once(() => {
  console.log("Инициализация!");
  return 42;
});

console.log(initialize()); // "Инициализация!", 42
console.log(initialize()); // 42 (без вывода в консоль)
```

---

## Асинхронность (`async-js.md`)

### Задание 1: Функция delay

```javascript
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function run() {
  console.log("Старт");
  await delay(1000);
  console.log("Середина");
  await delay(1000);
  console.log("Конец");
}

run();
```

### Задание 2: Загрузка пользователя

```javascript
async function fetchUserInfo(id) {
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`);
    if (!response.ok) throw new Error(`HTTP ошибка: ${response.status}`);

    const user = await response.json();
    return {
      name: user.name,
      email: user.email,
      city: user.address.city
    };
  } catch (error) {
    console.error("Ошибка загрузки:", error.message);
    return null;
  }
}

fetchUserInfo(1).then(user => console.log(user));
// { name: "Leanne Graham", email: "Sincere@april.biz", city: "Gwenborough" }
```

### Задание 3: Параллельная загрузка

```javascript
async function loadAllUsers(ids) {
  const promises = ids.map(id =>
    fetch(`https://jsonplaceholder.typicode.com/users/${id}`)
      .then(res => res.json())
      .then(user => ({ name: user.name, email: user.email }))
  );

  return Promise.all(promises);
}

loadAllUsers([1, 2, 3]).then(users => console.log(users));
// [
//   { name: "Leanne Graham", email: "Sincere@april.biz" },
//   { name: "Ervin Howell", email: "Shanna@melissa.tv" },
//   { name: "Clementine Bauch", email: "Nathan@yesenia.net" }
// ]
```

---

## Работа с DOM (`dom-manipulation.md`)

### Задание 1: Создание карточки

```javascript
function createCard(title, text, color) {
  const card = document.createElement("div");
  card.className = "card";
  card.style.backgroundColor = color;

  const h3 = document.createElement("h3");
  h3.textContent = title;

  const p = document.createElement("p");
  p.textContent = text;

  card.appendChild(h3);
  card.appendChild(p);

  return card;
}

// Использование:
const card = createCard("Заголовок", "Текст карточки", "#e0f7fa");
document.body.appendChild(card);
```

### Задание 2: Динамический список

```javascript
function addItem(listId, text) {
  const ul = document.getElementById(listId);

  const li = document.createElement("li");
  li.textContent = text;

  const btn = document.createElement("button");
  btn.textContent = "Удалить";
  btn.style.marginLeft = "10px";
  btn.addEventListener("click", () => li.remove());

  li.appendChild(btn);
  ul.appendChild(li);
}

// Использование:
addItem("myList", "Первый элемент");
addItem("myList", "Второй элемент");
```

### Задание 3: Подсветка элементов

```javascript
function highlightAll(selector, color) {
  const elements = document.querySelectorAll(selector);
  elements.forEach(el => {
    el.style.backgroundColor = color;
  });
}

highlightAll("p", "lightyellow");
```

---

## События (`events-js.md`)

### Задание 1: Кнопка-счётчик

```javascript
const button = document.createElement("button");
let count = 0;
button.textContent = "Кликов: 0";

button.addEventListener("click", () => {
  count++;
  button.textContent = `Кликов: ${count}`;
});

document.body.appendChild(button);
```

### Задание 2: Валидация поля ввода

```javascript
const input = document.createElement("input");
input.placeholder = "Введите текст (минимум 2 символа)";

input.addEventListener("input", () => {
  if (input.value.length >= 2) {
    input.style.border = "2px solid green";
  } else {
    input.style.border = "2px solid red";
  }
});

document.body.appendChild(input);
```

### Задание 3: Горячие клавиши

```javascript
document.addEventListener("keydown", (e) => {
  if (e.ctrlKey && e.key === "b") {
    e.preventDefault();
    document.body.classList.toggle("bold");
  }

  if (e.ctrlKey && e.key === "i") {
    e.preventDefault();
    document.body.classList.toggle("italic");
  }
});

// CSS-классы (добавь в <style>):
// .bold { font-weight: bold; }
// .italic { font-style: italic; }
```

---

## Даты (`dates-js.md`)

### Задание 1: Форматирование даты

```javascript
function formatDateRu(date) {
  const day = String(date.getDate()).padStart(2, "0");
  const month = String(date.getMonth() + 1).padStart(2, "0");
  const year = date.getFullYear();
  const hours = String(date.getHours()).padStart(2, "0");
  const minutes = String(date.getMinutes()).padStart(2, "0");

  return `${day}.${month}.${year} ${hours}:${minutes}`;
}

console.log(formatDateRu(new Date(2023, 0, 5, 9, 3))); // "05.01.2023 09:03"
```

### Задание 2: Точный возраст

```javascript
function getAge(birthDateStr) {
  const birth = new Date(birthDateStr);
  const today = new Date();

  let age = today.getFullYear() - birth.getFullYear();

  // Проверяем, прошёл ли уже день рождения в этом году
  const monthDiff = today.getMonth() - birth.getMonth();
  if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birth.getDate())) {
    age--;
  }

  return age;
}

console.log(getAge("2000-06-15")); // Зависит от текущей даты
```

### Задание 3: Дни между датами

```javascript
function daysBetween(dateStr1, dateStr2) {
  const date1 = new Date(dateStr1);
  const date2 = new Date(dateStr2);
  const diffMs = Math.abs(date2 - date1);
  return Math.floor(diffMs / (1000 * 60 * 60 * 24));
}

console.log(daysBetween("2024-01-01", "2024-01-31")); // 30
console.log(daysBetween("2024-03-01", "2024-01-01")); // 60
```

### Задание 4: Рабочий или выходной?

```javascript
function isWeekend(date) {
  const day = date.getDay();
  return day === 0 || day === 6; // 0 = воскресенье, 6 = суббота
}

console.log(isWeekend(new Date("2024-01-06"))); // true (суббота)
console.log(isWeekend(new Date("2024-01-08"))); // false (понедельник)
```

---

## Обработка ошибок (`error-handling.md`)

### Задание 1: Безопасное деление

```javascript
function safeDivide(a, b) {
  if (b === 0) throw new Error("Деление на ноль");
  return a / b;
}

try {
  console.log(safeDivide(10, 2));  // 5
  console.log(safeDivide(10, 0));  // Ошибка!
} catch (error) {
  console.log("Ошибка:", error.message); // "Ошибка: Деление на ноль"
}
```

### Задание 2: Валидация возраста

```javascript
class ValidationError extends Error {
  constructor(message, field) {
    super(message);
    this.name = "ValidationError";
    this.field = field;
  }
}

function validateAge(age) {
  if (typeof age !== "number" || isNaN(age)) {
    throw new ValidationError("должен быть числом", "age");
  }
  if (age < 0) {
    throw new ValidationError("не может быть отрицательным", "age");
  }
  if (age > 150) {
    throw new ValidationError("слишком большое значение", "age");
  }
  return true;
}

// Проверка:
try {
  validateAge("двадцать");
} catch (e) {
  if (e instanceof ValidationError) {
    console.log(`${e.field}: ${e.message}`); // "age: должен быть числом"
  }
}

try {
  validateAge(-5);
} catch (e) {
  console.log(`${e.field}: ${e.message}`); // "age: не может быть отрицательным"
}
```

### Задание 3: Безопасный fetch

```javascript
async function safeJsonFetch(url) {
  try {
    const response = await fetch(url);
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    return await response.json();
  } catch (error) {
    console.error("safeJsonFetch ошибка:", error.message);
    return null;
  }
}

// Использование:
const data = await safeJsonFetch("https://jsonplaceholder.typicode.com/posts/1");
console.log(data); // { userId: 1, id: 1, title: "...", body: "..." } или null
```

---

## Регулярные выражения (`regex-js.md`)

### Задание 1: Валидация телефона

```javascript
const phoneRegex = /^(\+7|8)\(?\d{3}\)?-?\d{3}-?\d{2}-?\d{2}$/;

console.log(phoneRegex.test("+79991234567"));       // true
console.log(phoneRegex.test("89991234567"));        // true
console.log(phoneRegex.test("+7(999)123-45-67"));   // true
console.log(phoneRegex.test("8(999)123-45-67"));    // true
console.log(phoneRegex.test("123456"));              // false
```

### Задание 2: Извлечение email

```javascript
function extractEmails(text) {
  const regex = /[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/g;
  return text.match(regex) || [];
}

console.log(extractEmails("Пишите на test@mail.ru или admin@site.com"));
// ["test@mail.ru", "admin@site.com"]

console.log(extractEmails("Нет email здесь")); // []
```

### Задание 3: Маскировка карты

```javascript
function maskCard(number) {
  const digits = number.replace(/\D/g, ""); // Убираем всё кроме цифр
  const last4 = digits.slice(-4);
  return `****-****-****-${last4}`;
}

console.log(maskCard("1234567890123456"));   // "****-****-****-3456"
console.log(maskCard("1234-5678-9012-3456")); // "****-****-****-3456"
```

---

## JSON и API (`json-api.md`)

### Задание 1: JSON туда и обратно

```javascript
const user = {
  name: "Анна",
  age: 25,
  hobbies: ["чтение", "музыка", "плавание"]
};

// В JSON с красивым форматированием
const json = JSON.stringify(user, null, 2);
console.log(json);
// {
//   "name": "Анна",
//   "age": 25,
//   "hobbies": ["чтение", "музыка", "плавание"]
// }

// Обратно в объект
const parsed = JSON.parse(json);
console.log(parsed.hobbies[0]); // "чтение"
```

### Задание 2: Безопасное хранилище

```javascript
function saveData(key, data) {
  try {
    localStorage.setItem(key, JSON.stringify(data));
    return true;
  } catch (error) {
    console.error("Ошибка сохранения:", error.message);
    return false;
  }
}

function loadData(key) {
  try {
    const data = localStorage.getItem(key);
    if (data === null) return null;
    return JSON.parse(data);
  } catch (error) {
    console.error("Ошибка загрузки:", error.message);
    return null;
  }
}

// Использование:
saveData("settings", { theme: "dark", lang: "ru" });
const settings = loadData("settings");
console.log(settings); // { theme: "dark", lang: "ru" }
```

### Задание 3: Пост с комментариями

```javascript
async function getPostWithComments(postId) {
  const [postRes, commentsRes] = await Promise.all([
    fetch(`https://jsonplaceholder.typicode.com/posts/${postId}`),
    fetch(`https://jsonplaceholder.typicode.com/posts/${postId}/comments`)
  ]);

  const post = await postRes.json();
  const comments = await commentsRes.json();

  return { post, comments };
}

// Использование:
getPostWithComments(1).then(data => {
  console.log("Пост:", data.post.title);
  console.log("Комментариев:", data.comments.length);
});
// Пост: "sunt aut facere repellat provident..."
// Комментариев: 5
```

---

> **Помни:** Лучший способ научиться — написать код самостоятельно, а потом сравнить с ответом! Не копируй решения бездумно.
