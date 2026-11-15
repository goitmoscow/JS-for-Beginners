# Условия и ветвления JavaScript 🎯

> **📚 Для кого этот материал:** Для тех, кто хочет научиться принимать решения в коде.
>
> **🎯 Что ты узнаешь:** Как использовать if/else, switch и тернарный оператор для создания разных путей выполнения программы.
>
> **💡 Важно:** В примерах кода имена переменных написаны на английском языке (например: `name`, `age`, `user`). Это стандарт в программировании!

## 🎦 Что такое условия?

Представь условия как **развилку на дороге**:

🚦 **Светофор** = проверка условия  
➡️ **Поворот налево** = один путь кода  
➡️ **Поворот направо** = другой путь кода

```javascript
if (trafficLight === "зеленый") {
  go(); // Путь 1
} else {
  stop(); // Путь 2
}
```

## ✅ if - простое условие

### 🎯 Базовый синтаксис

```javascript
let age = 18;

if (age >= 18) {
  console.log("Доступ разрешен!");
  console.log("Вы можете войти на сайт");
}

// Если условие true - выполняется код в {}
// Если условие false - пропускаем блок {}
```

### 🎯 Условие с одной строкой (без {})

```javascript
let online = true;

if (online) console.log("Пользователь в сети"); // Одна строка без {}

// ⚠️ Внимание: работает только для ОДНОЙ следующей строки
if (online) console.log("Пользователь в сети");
console.log("Это выполнится ВСЕГДА!"); // ❌ Не зависит от условия!
```

## 🔄 if...else - два варианта

```javascript
let grade = 4;

if (grade >= 5) {
  console.log("Отлично!");
} else {
  console.log("Нужно стараться лучше");
}

// В зависимости от условия выполнится ТОЛЬКО ОДИН блок
```

## 🔀 if...else if...else - много вариантов

```javascript
let age = 25;

if (age < 12) {
  console.log("Ребенок");
} else if (age < 18) {
  console.log("Подросток");
} else if (age < 65) {
  console.log("Взрослый");
} else {
  console.log("Пожилой");
}

// Проверки идут по порядку, выполняется первый подходящий вариант
```

## 🎨 Вложенные условия

```javascript
let age = 20;
let hasLicense = false;

if (age >= 18) {
  if (hasLicense) {
    console.log("Можно водить машину!");
  } else {
    console.log("Нужно получить права");
  }
} else {
  console.log("Слишком молод для вождения");
}

// Можно упростить с помощью логических операторов:
if (age >= 18 && hasLicense) {
  console.log("Можно водить машину!");
} else if (age >= 18 && !hasLicense) {
  console.log("Нужно получить права");
} else {
  console.log("Слишком молод для вождения");
}
```

## 🎭 Таблица истинности для сложных условий

| Условие 1 | Условие 2 | `&&` (И) | `\|\|` (ИЛИ) |
| --------- | --------- | -------- | ------------- |
| true      | true      | true     | true          |
| true      | false     | false    | true          |
| false     | true      | false    | true          |
| false     | false     | false    | false         |

## 🔄 switch - переключатель для множества вариантов

### 🎯 Базовый синтаксис

```javascript
let day = "понедельник";

switch (day) {
  case "понедельник":
    console.log("Начало недели");
    break;
  case "среда":
    console.log("Середина недели");
    break;
  case "пятница":
    console.log("Почти выходные!");
    break;
  default:
    console.log("Обычный день");
}
```

### 🎯 switch с множественными case

```javascript
let grade = 4;

switch (grade) {
  case 5:
    console.log("Отлично!");
    break;
  case 4:
    console.log("Хорошо");
    break;
  case 3:
    console.log("Удовлетворительно");
    break;
  case 2:
  case 1:
    console.log("Плохо");
    break;
  default:
    console.log("Некорректная оценка");
}
```

### 🎯 switch без break (проваливание)

```javascript
let season = "зима";

switch (season) {
  case "зима":
    console.log("Декабрь");
  case "весна":
    console.log("Март");
    break; // Останавливаемся здесь
  case "лето":
    console.log("Июнь");
  case "осень":
    console.log("Сентябрь");
    break;
}

// Вывод для "зима":
// "Декабрь"
// "Март"
```

### ⚠️ Что будет без break?

```javascript
let fruit = "яблоко";

switch (fruit) {
  case "яблоко":
    console.log("Красное яблоко");
  case "банан":
    console.log("Желтый банан");
    break;
  default:
    console.log("Неизвестный фрукт");
}

// Вывод:
// "Красное яблоко"
// "Желтый банан" (выведется тоже, потому что нет break!)
```

## ⚡ Тернарный оператор - короткое if

### 🎯 Базовый синтаксис

```javascript
let age = 18;
let status = age >= 18 ? "совершеннолетний" : "несовершеннолетний";
console.log(status); // "совершеннолетний"

// То же самое с if:
let status2;
if (age >= 18) {
  status2 = "совершеннолетний";
} else {
  status2 = "несовершеннолетний";
}
```

### 🎯 Вложенные тернарные операторы

```javascript
let grade = 3;
let result =
  grade === 5
    ? "отлично"
    : grade === 4
      ? "хорошо"
      : grade === 3
        ? "удовлетворительно"
        : "плохо";
console.log(result); // "удовлетворительно"
```

### 🎯 Тернарный оператор в действиях

```javascript
let online = true;
online ? console.log("Добро пожаловать!") : console.log("Войдите в систему");

// Выполнение функции
let user = null;
let name = user ? user.name : "Гость"; // "Гость" (без ошибки!)
```

## 🎯 Практические примеры

### 🎮 Проверка пароля

```javascript
function validatePassword(password) {
  if (!password) {
    return "Введите пароль";
  }

  if (password.length < 6) {
    return "Слишком короткий пароль";
  }

  if (!/\p{Lu}/u.test(password)) {
    return "Нужна заглавная буква";
  }

  if (!/[0-9]/.test(password)) {
    return "Нужна цифра";
  }

  return "Пароль соответствует учебным условиям";
}

console.log(validatePassword("123")); // "Слишком короткий пароль"
console.log(validatePassword("пароль")); // "Нужна заглавная буква"
console.log(validatePassword("Пароль")); // "Нужна цифра"
console.log(validatePassword("Пароль123")); // "Пароль соответствует учебным условиям"
```

### 🛒 Калькулятор скидок

```javascript
function calculatePrice(price, quantity, client) {
  let totalPrice = price * quantity;
  let discount = 0;

  // Скидка за количество
  if (quantity >= 10) {
    discount = 15;
  } else if (quantity >= 5) {
    discount = 10;
  } else if (quantity >= 3) {
    discount = 5;
  }

  // Дополнительная скидка для постоянных клиентов
  if (client === "постоянный") {
    discount += 5;
  }

  // Максимальная скидка 30%
  if (discount > 30) discount = 30;

  let total = totalPrice * (1 - discount / 100);

  return {
    basePrice: totalPrice,
    discount: discount,
    finalPrice: total,
    savings: totalPrice - total,
  };
}

let order = calculatePrice(1000, 8, "постоянный");
console.log(order);
// {
//   basePrice: 8000,
//   discount: 15,
//   finalPrice: 6800,
//   savings: 1200
// }
```

### 📊 Определение времени суток

```javascript
function greetingByTime(hours) {
  if (!Number.isInteger(hours) || hours < 0 || hours > 23) return "Некорректное время";
  let timeOfDay;

  if (hours >= 6 && hours < 12) {
    timeOfDay = "утро";
  } else if (hours >= 12 && hours < 18) {
    timeOfDay = "день";
  } else if (hours >= 18 && hours < 22) {
    timeOfDay = "вечер";
  } else if (hours >= 22 || hours < 6) {
    timeOfDay = "ночь";
  } else {
    timeOfDay = "неизвестное время";
  }

  switch (timeOfDay) {
    case "утро":
      return `Доброе утро! Сейчас ${hours} часов`;
    case "день":
      return `Добрый день! Сейчас ${hours} часов`;
    case "вечер":
      return `Добрый вечер! Сейчас ${hours} часов`;
    case "ночь":
      return `Доброй ночи! Сейчас ${hours} часов`;
    default:
      return "Некорректное время";
  }
}

console.log(greetingByTime(8)); // "Доброе утро! Сейчас 8 часов"
console.log(greetingByTime(15)); // "Добрый день! Сейчас 15 часов"
```

### 🎮 Калькулятор с проверками

```javascript
function calculator(a, operator, b) {
  // Проверка чисел
  if (!Number.isFinite(a) || !Number.isFinite(b)) {
    return "Оба аргумента должны быть числами";
  }

  // Проверка деления на ноль
  if (operator === "/" && b === 0) {
    return "Деление на ноль невозможно";
  }

  // Вычисление
  let result;
  switch (operator) {
    case "+":
      result = a + b;
      break;
    case "-":
      result = a - b;
      break;
    case "*":
      result = a * b;
      break;
    case "/":
      result = a / b;
      break;
    case "**":
      result = a ** b;
      break;
    default:
      return "Неизвестный оператор";
  }

  return result;
}

console.log(calculator(5, "+", 3)); // 8
console.log(calculator(10, "/", 2)); // 5
console.log(calculator(2, "**", 3)); // 8
console.log(calculator(5, "/", 0)); // "Деление на ноль невозможно"
console.log(calculator(5, "xxx", 2)); // "Неизвестный оператор"
```

## 🎯 Короткая запись с логическими операторами

### ⚡ ИЛИ (||) как значение по умолчанию

```javascript
let name = null;
let userName = name || "Гость"; // "Гость"

let age = 25;
let userAge = age || 18; // 25 (переменная есть)

// Проверка нескольких вариантов
let title = null;
let title2 = "";
let title3 = "Продукт";

let finalTitle = title || title2 || title3 || "Без названия";
// "Продукт"
```

### ⚡ И (&&) для проверки с действием

```javascript
let user = { name: "Анна", age: 25 };

// Безопасное получение вложенного свойства
let city = user && user.address && user.address.city;
// undefined (без ошибки!)

// Выполнение действия при условии
online && sendMessage(); // Отправит только если онлайн = true
```

## 🚨 Частые ошибки новичков

### ❌ Забытые фигурные скобки

```javascript
let age = 18;

// ❌ ПЛОХО - путаница с отступами
if (age >= 18) console.log("Доступ разрешен");
console.log("Эта строка выполнится всегда!");

// ✅ ХОРОШО - всегда используй фигурные скобки
if (age >= 18) {
  console.log("Доступ разрешен");
  console.log("Эта строка выполнится только если условие true");
}
```

### ❌ Путаница = и ==

```javascript
let online = true;

// ❌ ПЛОХО - присваивание вместо сравнения
if ((online = false)) {
  // Всегда false!
  console.log("Не выполнится никогда");
}

// ✅ ХОРОШО - сравнение
if (online === false) {
  console.log("Пользователь оффлайн");
}
```

### ❌ Забытый break в switch

```javascript
let fruit = "яблоко";

// ❌ ПЛОХО - проваливание случаев
switch (fruit) {
  case "яблоко":
    console.log("Яблоко"); // Выведется
  case "банан":
    console.log("Банан"); // И это выведется!
}

// ✅ ХОРОШО - с break
switch (fruit) {
  case "яблоко":
    console.log("Яблоко");
    break;
  case "банан":
    console.log("Банан");
    break;
}
```

### ❌ Слишком сложные условия

```javascript
let age = 25;
let student = true;
let online = true;

// ❌ ПЛОХО - сложно читать
if (age >= 18 && (student || online)) {
  console.log("Доступ разрешен");
}

// ✅ ХОРОШО - с промежуточными переменными
let isAdult = age >= 18;
let isActive = student || online;
let isAccessAllowed = isAdult && isActive;

if (isAccessAllowed) {
  console.log("Доступ разрешен");
}
```

## 📚 Шпаргалка выбора конструкции

| Ситуация                   | Рекомендация       | Пример                                       |
| -------------------------- | ------------------ | -------------------------------------------- |
| 2 варианта выбора          | `if-else`          | `if (x > 0) { ... } else { ... }`            |
| Больше 2 вариантов         | `if-else if-else`  | `if (x < 0) { ... } else if (x > 0) { ... }` |
| Сравнение одной переменной | `switch`           | `switch (день) { case "пн": ... }`           |
| Короткое присваивание      | Тернарный оператор | `let x = y > 0 ? "плюс" : "минус"`           |
| Значение по умолчанию | `\|\|` / `??` | `const x = y ?? "по умолчанию"` |
| Условное действие          | `&&`               | `x && doSomething()`                      |

## 📚 Шпаргалка операторов сравнения

| Оператор | Значение          | Когда использовать                      |
| -------- | ----------------- | --------------------------------------- |
| `===`    | Строго равно      | Всегда!                                 |
| `!==`    | Строго не равно   | Всегда!                                 |
| `==`     | Нестрого равно    | Только при необходимости преобразования |
| `!=`     | Нестрого не равно | Редко                                   |
| `>`      | Больше            | Числовые сравнения                      |
| `<`      | Меньше            | Числовые сравнения                      |
| `>=`     | Больше или равно  | Числовые сравнения                      |
| `<=`     | Меньше или равно  | Числовые сравнения                      |

## 🎮 Практика в консоли

Открой F12 и попробуй:

```javascript
// 1. Возрастная категория
let age = prompt("Сколько тебе лет?");
if (age >= 18) {
  console.log("Ты взрослый");
} else {
  console.log("Ты еще молодой");
}

// 2. Оценка в буквенной системе
let number = 85;
let grade;
if (number >= 90) {
  grade = "A";
} else if (number >= 80) {
  grade = "B";
} else if (number >= 70) {
  grade = "C";
} else {
  grade = "D";
}
console.log(`Оценка: ${grade}`);

// 3. Тернарный оператор
let time = 14;
let greeting = time < 12 ? "Доброе утро" : "Добрый день";
console.log(greeting);

// 4. Switch
let dayOfWeek = "пятница";
switch (dayOfWeek) {
  case "понедельник":
  case "вторник":
  case "среда":
  case "четверг":
  case "пятница":
    console.log("Рабочий день");
    break;
  case "суббота":
  case "воскресенье":
    console.log("Выходной");
    break;
}
```


## 📝 Задания для закрепления

### Задание 1: Время года
Напиши функцию `getSeason(month)`, которая принимает номер месяца (1-12) и возвращает время года: "зима", "весна", "лето", "осень". Для некорректного месяца верни "неизвестный месяц".

### Задание 2: Цена билета
Напиши функцию `getTicketPrice(age, isStudent)`, которая возвращает цену билета в кино:
- Дети до 12 лет — бесплатно (0)
- Студенты — 200
- Пенсионеры (65+) — 150
- Остальные взрослые — 400

### Задание 3: Тернарный оператор
Перепиши следующий код с использованием тернарного оператора (в одну строку):
```javascript
let temperature = 25;
let weather;
if (temperature > 30) {
  weather = "жарко";
} else if (temperature > 20) {
  weather = "тепло";
} else if (temperature > 10) {
  weather = "прохладно";
} else {
  weather = "холодно";
}
```

### Задание 4: Калькулятор на switch
Напиши функцию `calc(a, operator, b)` используя `switch`, которая поддерживает операции: `+`, `-`, `*`, `/`, `%`. При делении на 0 верни `"Ошибка: деление на ноль"`. Для неизвестного оператора верни `"Неизвестный оператор"`.

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** Условия - это как развилки на дороге! Они позволяют программе выбирать правильный путь в зависимости от ситуации. 🛤️

Используй `===` вместо `==` и не забывай про `break` в `switch`! 🎯

---

[⬅️ Предыдущая тема: Операторы](operators-js.md) | [📚 Оглавление](README.md) | [Следующая тема: Функции ➡️](function.md)
