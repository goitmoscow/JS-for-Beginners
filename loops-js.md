# Циклы JavaScript 🔄

> **📚 Для кого этот материал:** Для тех, кто хочет научиться повторять действия без копирования кода.
>
> **🎯 Что ты узнаешь:** Разные типы циклов (for, while, for...of), как их использовать и когда какой выбрать.
>
> **💡 Важно:** В примерах кода имена переменных написаны на английском языке (например: `name`, `age`, `user`). Это стандарт в программировании!

## 🎦 Что такое цикл?

Представь цикл как **повторяющиеся действия**:

🔄 **Повторить 5 раз** = сделать что-то 5 раз подряд  
⏰ **Пока условие истинно** = повторять до тех пор, пока что-то не изменится  
📋 **Для каждого элемента** = сделать действие для каждого предмета в списке

```javascript
// Повторить "привет" 3 раза:
for (let i = 0; i < 3; i++) {
  console.log("привет"); // выполнится 3 раза
}
```

## 🎯 for - классический цикл со счетчиком

### 🔢 Базовый синтаксис

```javascript
for (let i = 0; i < 5; i++) {
  // 1. let i = 0      - начальное значение
  // 2. i < 5           - условие продолжения
  // 3. i++             - действие после каждой итерации
  console.log(`Итерация ${i}`);
}

// Вывод:
// Итерация 0
// Итерация 1
// Итерация 2
// Итерация 3
// Итерация 4
```

### 📊 Подробное объяснение работы

```javascript
for (let i = 1; i <= 3; i++) {
  console.log(`Шаг ${i}`);
}

// Пошаговое выполнение:
// 1. i = 1 (инициализация)
// 2. 1 <= 3? Да → выполняем console.log("Шаг 1")
// 3. i = 2 (i++)
// 4. 2 <= 3? Да → выполняем console.log("Шаг 2")
// 5. i = 3 (i++)
// 6. 3 <= 3? Да → выполняем console.log("Шаг 3")
// 7. i = 4 (i++)
// 8. 4 <= 3? Нет → цикл заканчивается
```

### 🎯 Разные варианты for

```javascript
// От 5 до 1 (обратный отсчет)
for (let i = 5; i >= 1; i--) {
  console.log(i);
}

// Шаг 2 (только четные)
for (let i = 0; i <= 10; i += 2) {
  console.log(i);
}

// Цикл по строке
let text = "Привет";
for (let i = 0; i < text.length; i++) {
  console.log(text[i]);
}
```

## 🔢 for...of - цикл по элементам (современный)

### 🎯 Массивы

```javascript
let fruits = ["яблоко", "банан", "апельсин"];

for (let fruit of fruits) {
  console.log(`Фрукт: ${fruit}`);
}
// Фрукт: яблоко
// Фрукт: банан
// Фрукт: апельсин
```

### 🎯 Строки

```javascript
let word = "JavaScript";

for (let letter of word) {
  console.log(letter);
}
// J
// a
// v
// a
// S
// c
// r
// i
// p
// t
```

### 🎯 Получение индекса с entries()

```javascript
let colors = ["красный", "зеленый", "синий"];

for (let [index, color] of colors.entries()) {
  console.log(`${index}: ${color}`);
}
// 0: красный
// 1: зеленый
// 2: синий
```

## 🔑 for...in - цикл по ключам объекта

```javascript
let person = {
  name: "Елена",
  age: 28,
  city: "Москва",
};

for (let key in person) {
  console.log(`${key}: ${person[key]}`);
}
// name: Елена
// age: 28
// city: Москва
```

### ⚠️ Внимание: for...in и массивы!

```javascript
let array = [10, 20, 30];

// ❌ НЕ РЕКОМЕНДУЕТСЯ для массивов
for (let index in array) {
  console.log(index, array[index]); // работает, но есть нюансы
}

// ✅ ИСПОЛЬЗУЙТЕ for...of для массивов
for (let element of array) {
  console.log(element);
}
```

## ⏰ while - цикл с условием

### 🔁 Базовый синтаксис

```javascript
let counter = 0;

while (counter < 3) {
  console.log(`Счетчик: ${counter}`);
  counter++; // Очень важно менять переменную!
}

// Счетчик: 0
// Счетчик: 1
// Счетчик: 2
```

### ⚠️ Опасность бесконечного цикла

```javascript
// ❌ БЕСКОНЕЧНЫЙ ЦИКЛ!
let error = 0;
while (error < 3) {
  console.log("Это будет работать вечно");
  // Забыли error++ → переменная не меняется
}
```

### 🎯 Практический пример

```javascript
// Ищем случайное число больше 50
let random = 0;
let attempts = 0;

while (random <= 50 && attempts < 10) {
  random = Math.random() * 100;
  attempts++;
  console.log(`Попытка ${attempts}: ${random.toFixed(2)}`);
}

if (random > 50) {
  console.log(`Найдено число: ${random.toFixed(2)}`);
} else {
  console.log("За 10 попыток подходящее число не найдено");
}
```

## ⏰ do...while - цикл с постусловием

```javascript
let number;

do {
  number = Math.floor(Math.random() * 10);
  console.log(`Выпало: ${number}`);
} while (number !== 0);

// В отличие от while, выполняется ХОТЯ БЫ ОДИН РАЗ!
```

### 🔀 Разница while vs do...while

```javascript
let condition = false;

// while - может не выполниться ни разу
while (condition) {
  console.log("Не выполнится");
}

// do...while - выполнится хотя бы один раз
do {
  console.log("Выполнится один раз");
} while (condition);
```

## 🎯 forEach - метод массива

```javascript
let numbers = [1, 2, 3, 4, 5];

// Базовый вариант
numbers.forEach(function (element, index, array) {
  console.log(`${index}: ${element}`);
});

// Современный вариант со стрелочной функцией
numbers.forEach((element, index) => {
  console.log(`${index}: ${element}`);
});

// Только элементы
numbers.forEach((element) => {
  console.log(element);
});
```

### 🎯 Особенности forEach

```javascript
// ❌ НЕЛЬЗЯ использовать break или continue
numbers.forEach(element => {
    if (element === 3) {
        break; // ❌ ОШИБКА!
    }
});

// Для break/continue используйте for...of
for (let element of numbers) {
    if (element === 3) {
        break; // ✅ Работает!
    }
}
```

## 🛑 Управление циклами

### ⏹️ break - выход из цикла

```javascript
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break; // Выходим из цикла при i === 5
  }
  console.log(i);
}
// 0, 1, 2, 3, 4
```

### ⏭️ continue - пропуск итерации

```javascript
for (let i = 0; i < 5; i++) {
  if (i === 2) {
    continue; // Пропускаем i === 2
  }
  console.log(i);
}
// 0, 1, 3, 4
```

### 🏷️ Метки для вложенных циклов

```javascript
outer: for (let i = 0; i < 3; i++) {
  inner: for (let j = 0; j < 3; j++) {
    if (i === 1 && j === 1) {
      break outer; // Выход из ВНЕШНЕГО цикла
    }
    console.log(`${i},${j}`);
  }
}
// 0,0  0,1  0,2  1,0
```

## 🎯 Практические примеры

### 📊 Подсчет суммы чисел

```javascript
let numbers = [1, 2, 3, 4, 5];
let sum = 0;

// Способ 1: for
for (let i = 0; i < numbers.length; i++) {
  sum += numbers[i];
}

// Способ 2: for...of
sum = 0;
for (let number of numbers) {
  sum += number;
}

// Способ 3: forEach
sum = 0;
numbers.forEach((number) => (sum += number));

console.log(`Сумма: ${sum}`); // 15
```

### 🎯 Поиск максимального элемента

```javascript
let grades = [3, 5, 4, 2, 5, 4, 3];
let maximum = grades[0];

for (let grade of grades) {
  if (grade > maximum) {
    maximum = grade;
  }
}

console.log(`Максимальная оценка: ${maximum}`); // 5
```

### 🎮 Фильтрация массива

```javascript
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let even = [];

for (let number of numbers) {
  if (number % 2 === 0) {
    even.push(number);
  }
}

console.log(even); // [2, 4, 6, 8, 10]
```

### 📝 Создание таблицы умножения

```javascript
let size = 5;

for (let i = 1; i <= size; i++) {
  let row = "";
  for (let j = 1; j <= size; j++) {
    row += (i * j).toString().padStart(4, " ");
  }
  console.log(row);
}

// Вывод:
//   1   2   3   4   5
//   2   4   6   8  10
//   3   6   9  12  15
//   4   8  12  16  20
//   5  10  15  20  25
```

### 🔍 Поиск в объектах

```javascript
let users = [
  { id: 1, name: "Анна", age: 25 },
  { id: 2, name: "Борис", age: 30 },
  { id: 3, name: "Виктор", age: 35 },
];

let searchId = 2;
let foundUser = null;

for (let user of users) {
  if (user.id === searchId) {
    foundUser = user;
    break; // Нашли - выходим из цикла
  }
}

if (foundUser) {
  console.log(`Найден: ${foundUser.name}`);
} else {
  console.log("Пользователь не найден");
}
```

### 🎲 Игра "Угадай число"

```javascript
let secret = Math.floor(Math.random() * 100) + 1;
let guess;
let attempts = 0;
let maxAttempts = 7;

while (attempts < maxAttempts) {
  const input = prompt(`Попытка ${attempts + 1}/${maxAttempts}. Введите число (1-100):`);
  if (input === null) break; // Отмена завершает игру
  guess = Number(input);

  if (input.trim() === "" || !Number.isInteger(guess) || guess < 1 || guess > 100) {
    console.log("Введите корректное число!");
    continue;
  }

  attempts++;

  if (guess === secret) {
    console.log(
      `🎉 Поздравляю! Вы угадали число ${secret} за ${attempts} попыток!`,
    );
    break;
  } else if (guess < secret) {
    console.log("📈 Слишком мало!");
  } else {
    console.log("📉 Слишком много!");
  }
}

if (attempts >= maxAttempts && guess !== secret) {
  console.log(`😢 Игра окончена! Загаданное число было: ${secret}`);
}
```

## 🚨 Частые ошибки новичков

### ❌ Бесконечный цикл

```javascript
let i = 0;
while (i < 5) {
  console.log(i);
  // ❌ Забыли i++ → бесконечный цикл!
}
```

### ❌ Ошибка "off-by-one"

```javascript
let array = [1, 2, 3];

// ❌ ПЛОХО - выйдет за пределы массива
for (let i = 0; i <= array.length; i++) {
  console.log(array[i]); // Последний раз будет undefined
}

// ✅ ХОРОШО
for (let i = 0; i < array.length; i++) {
  console.log(array[i]);
}
```

### ❌ Изменение массива при обходе

```javascript
let numbers = [1, 2, 3, 4, 5];

// ❌ ПЛОХО - нарушаем индексацию
for (let i = 0; i < numbers.length; i++) {
  if (numbers[i] % 2 === 0) {
    numbers.splice(i, 1); // Пропустим следующий элемент!
  }
}

// ✅ ХОРОШО - создаем новый массив
let odd = [];
for (let number of numbers) {
  if (number % 2 !== 0) {
    odd.push(number);
  }
}
```

### ❌ Путаница for...in и for...of

```javascript
let array = [10, 20, 30];

// ❌ НЕПРАВИЛЬНО для массива
for (let index in array) {
  console.log(index); // "0", "1", "2" как строки!
}

// ✅ ПРАВИЛЬНО для массива
for (let element of array) {
  console.log(element); // 10, 20, 30
}

// ✅ ПРАВИЛЬНО для объекта
let object = { a: 1, b: 2 };
for (let key in object) {
  console.log(key, object[key]); // a 1, b 2
}
```

## 📚 Шпаргалка выбора цикла

| Задача                         | Рекомендация | Пример                                 |
| ------------------------------ | ------------ | -------------------------------------- |
| Итерация с индексом            | `for`        | `for (let i = 0; i < arr.length; i++)` |
| Обход массива                  | `for...of`   | `for (let item of arr)`                |
| Обход объекта                  | `for...in`   | `for (let key in obj)`                 |
| Цикл по условию                | `while`      | `while (condition)`                    |
| Хоть один раз                  | `do...while` | `do { ... } while (condition)`         |
| Выполнить действие для каждого | `forEach()`  | `arr.forEach(item => ...)`             |

## 📚 Шпаргалка по управлению

| Оператор   | Действие            | Когда использовать           |
| ---------- | ------------------- | ---------------------------- |
| `break`    | Выйти из цикла      | Нашли нужный элемент         |
| `continue` | Пропустить итерацию | Пропускаем ненужные элементы |
| `метка:`   | Выйти из вложенного | Сложные вложенные циклы      |

## 🎮 Практика в консоли

Открой F12 и попробуй:

```javascript
// 1. Таблица умножения
for (let i = 1; i <= 5; i++) {
  for (let j = 1; j <= 5; j++) {
    console.log(`${i} × ${j} = ${i * j}`);
  }
  console.log("---"); // Разделитель
}

// 2. Поиск четных чисел
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let even = [];
for (let number of numbers) {
  if (number % 2 === 0) {
    even.push(number);
  }
}
console.log("Четные:", even);

// 3. Сумма цифр числа
let number = 12345;
let sum = 0;
for (let digit of number.toString()) {
  sum += parseInt(digit);
}
console.log(`Сумма цифр ${number} = ${sum}`);

// 4. Обратный отсчет
let countdown = 10;
while (countdown >= 0) {
  console.log(countdown);
  countdown--;
}
console.log("Пуск!");

// 5. Поиск в массиве объектов
let products = [
  { name: "Яблоко", price: 50 },
  { name: "Банан", price: 30 },
  { name: "Апельсин", price: 70 },
];
let budget = 40;
for (let product of products) {
  if (product.price <= budget) {
    console.log(`Можно купить: ${product.name}`);
  }
}
```


## 📝 Задания для закрепления

### Задание 1: FizzBuzz
Напиши программу, которая для чисел от 1 до 30 выводит:
- `"Fizz"` — если число делится на 3
- `"Buzz"` — если число делится на 5
- `"FizzBuzz"` — если делится на оба
- Само число — в остальных случаях

### Задание 2: Переворот строки
Напиши функцию `reverseString(str)`, которая переворачивает строку с помощью цикла (без метода `.reverse()`).
```javascript
reverseString("hello"); // "olleh"
reverseString("JavaScript"); // "tpircSavaJ"
```

### Задание 3: Пирамида
Напиши программу, которая выводит пирамиду из символов `*` высотой `n`:
```
*
**
***
****
*****
```

### Задание 4: Поиск дубликатов
Напиши функцию `findDuplicates(array)`, которая возвращает массив элементов, встречающихся более одного раза.
```javascript
findDuplicates([1, 2, 3, 2, 4, 3, 5]); // [2, 3]
```

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** Циклы - это как повторяющиеся движения! Они позволяют делать однотипные действия много раз без копирования кода. 🔄

Выбирай правильный тип цикла для задачи, и твой код станет чище и эффективнее! 🎯

---

[⬅️ Предыдущая тема: Функции](function.md) | [📚 Оглавление](README.md) | [Следующая тема: Строки ➡️](strings-js.md)
