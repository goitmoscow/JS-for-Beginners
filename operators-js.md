# Операторы JavaScript ⚡

> **📚 Для кого этот материал:** Для новичков, изучающих математические и логические операции.
>
> **🎯 Что ты узнаешь:** Как складывать, вычитать, сравнивать значения и использовать логику.
>
> **💡 Важно:** В примерах кода имена переменных написаны на английском языке (например: `name`, `age`, `user`). Это стандарт в программировании!

## 🎦 Что такое операторы?

Представь операторы как **знаки операций в математике**:

➕ **Сложение** = объединить значения  
➖ **Вычитание** = отнять значение  
✖️ **Умножение** = повторить значение много раз  
✅ **Сравнение** = проверить, больше/меньше/равно

```javascript
let result = 5 + 3; // ➕ оператор + складывает числа
let check = 5 > 3; // ✅ оператор > сравнивает числа
```

## 🔢 Арифметические операторы

### ➕ Сложение

```javascript
let apples = 5;
let oranges = 3;
let fruits = apples + oranges; // 8

// Со строками - склеивание
let greeting = "Привет";
let world = "мир";
let phrase = greeting + ", " + world; // "Привет, мир"

// Число + строка = строка!
let mix = 5 + " яблок"; // "5 яблок"
let anotherMix = "яблок: " + 5; // "яблок: 5"
```

### ➖ Вычитание

```javascript
let money = 1000;
let expenses = 350;
let remainder = money - expenses; // 650

// Со строками - автоматическое преобразование
let result = "100" - "50"; // 50 (работает!)
let error = "привет" - 5; // NaN (Not a Number)
```

### ✖️ Умножение

```javascript
let price = 150;
let quantity = 3;
let cost = price * quantity; // 450

// С дробными числами
let height = 1.75;
let weight = 70;
let index = weight / (height * height); // Расчет индекса массы
```

### ➗ Деление

```javascript
let cake = 8;
let guests = 4;
let piecesPerGuest = cake / guests; // 2

// Деление на ноль
let infinity = 5 / 0; // Infinity
let negativeInfinity = -5 / 0; // -Infinity
let notANumber = 0 / 0; // NaN
```

### 📦 Остаток от деления (modulo)

```javascript
// Проверка четности
let number = 7;
let isEven = number % 2 === 0; // false (7 - нечетное)
let number2 = 8;
let isEven2 = number2 % 2 === 0; // true (8 - четное)

// Остатки в реальной жизни
let apples = 23;
let fullBoxes = Math.floor(apples / 10); // 2 ящика
let remainingApples = apples % 10; // 3 яблока
```

### 🔼 Возведение в степень

```javascript
let base = 2;
let power = 3;
let result = base ** power; // 8 (2³)

// Квадрат числа
let number = 5;
let square = number ** 2; // 25

// Корень числа
let squareRoot = 16 ** 0.5; // 4
let cubeRoot = 27 ** (1 / 3); // 3
```

## ⚡ Сокращенные операторы присваивания

### 🔄 Увеличение/уменьшение на 1

```javascript
let counter = 0;

// Увеличение (инкремент)
counter++; // counter = 1
++counter; // counter = 2

// Уменьшение (декремент)
counter--; // counter = 1
--counter; // counter = 0

// Разница в положении ++
let a = 5;
let b = a++; // b = 5, потом a = 6 (постфикс)

let c = 5;
let d = ++c; // c = 6, потом d = 6 (префикс)
```

### 🔄 Математические сокращения

```javascript
let balance = 1000;

// += прибавить к существующему
balance += 500; // balance = 1500 (то же самое, что balance = balance + 500)

// -= отнять от существующего
balance -= 200; // balance = 1300 (то же самое, что balance = balance - 200)

// *= умножить существующее
balance *= 2; // balance = 2600 (то же самое, что balance = balance * 2)

// /= разделить существующее
balance /= 4; // balance = 650 (то же самое, что balance = balance / 4)

// %= остаток от деления
balance %= 100; // balance = 50 (то же самое, что balance = balance % 100)
```

## 🔍 Операторы сравнения

### 📏 Простые сравнения

```javascript
let a = 5;
let b = 10;

// Равно (преобразует типы)
console.log(5 == "5"); // true (строку "5" преобразует в число 5)

// Строго равно (без преобразования типов)
console.log(5 === "5"); // false (число не равно строке)

// Не равно
console.log(5 != "5"); // false (после преобразования они равны)

// Строго не равно
console.log(5 !== "5"); // true (число не равно строке)

// Больше/меньше
console.log(10 > 5); // true
console.log(5 < 10); // true

// Больше или равно/меньше или равно
console.log(5 >= 5); // true
console.log(5 <= 5); // true
```

### ⚠️ Особые случаи сравнения

```javascript
// Сравнение с null и undefined
null == undefined; // true (особый случай)
null === undefined; // false

// Сравнение с NaN
NaN == NaN; // false (NaN не равен ничему, даже самому себе)
Number.isNaN(NaN); // true (проверка без преобразования типов)

// Строки сравниваются лексикографически
"apple" < "banana"; // true ('a' < 'b')
"zoo" > "apple"; // true ('z' > 'a')
"10" < "2"; // true ('1' < '2' как символы!)
```

## 🧠 Логические операторы

### ✅ Логическое И (AND) - &&

Вычисляет слева направо: возвращает первый falsy-операнд, а если такого нет — последний. Остаток выражения после остановки не выполняется. Результат не обязательно boolean.

```javascript
// Оба условия должны быть true
let age = 25;
let hasLicense = true;
let canDrive = age >= 18 && hasLicense; // true

// Если хоть одно false, результат false
let age2 = 16;
let canDrive2 = age2 >= 18 && hasLicense; // false

// Короткое замыкание (short circuit)
let user = null;
let name = user && user.name; // null (не будет пытаться получить имя)
```

### ⚡ Логическое ИЛИ (OR) - ||

Возвращает первый truthy-операнд, а если такого нет — последний. Значения 0 и "" тоже заменяются при выборе через ||. Чтобы заменять только null и undefined, используйте ??.

```javascript
// Хотя бы одно условие должно быть true
let online = false;
let onPause = true;
let canWrite = online || onPause; // true

// Значение по умолчанию
let name = null;
let userName = name || "Гость"; // "Гость"

// Короткое замыкание
let user2 = { name: "Анна" };
let name2 = user2 || "Гость"; // { name: "Анна" } (объект truthy)
```

### 🔄 Логическое НЕ (NOT) - !

```javascript
let online = true;
let offline = !online; // false

let emptyString = "";
let notEmpty = !emptyString; // true (пустая строка = false)

let number = 0;
let notZero = !number; // true (0 = false)

// Двойное отрицание - преобразование в boolean
console.log(!!"привет"); // true
console.log(!!0); // false
console.log(!!null); // false
console.log(!!{}); // true
```

## 🎯 Таблица истинности

| A     | B     | A `&&` B | A `\|\|` B | `!`A  |
| ----- | ----- | -------- | ---------- | ----- |
| true  | true  | true     | true       | false |
| true  | false | false    | true       | false |
| false | true  | false    | true       | true  |
| false | false | false    | false      | true  |

## 🎭 Truthy и Falsy значения

### 🚫 Falsy (всегда false в логическом контексте)

- `false`
- `0`, `-0` и `0n` (BigInt ноль)
- `""` (пустая строка)
- `null`
- `undefined`
- `NaN`

### ✅ Truthy (всегда true в логическом контексте)

- Все остальные значения
- `"0"` (строка с нулем)
- `[]` (пустой массив)
- `{}` (пустой объект)
- `"false"` (строка "false")

```javascript
// Примеры
if (0) {
  console.log("не выполнится");
} // false
if ("0") {
  console.log("выполнится");
} // true
if ([]) {
  console.log("выполнится");
} // true
if ({}) {
  console.log("выполнится");
} // true
```

## 🔗 Операторы для строк

### ➕ Конкатенация (сложение строк)

```javascript
let name = "Иван";
let lastName = "Петров";
let fullName = name + " " + lastName; // "Иван Петров"

// Со сложением чисел
let age = 25;
let text = "Мне " + age + " лет"; // "Мне 25 лет"
```

### 📏 Сравнение строк

```javascript
"apple" < "banana"; // true (лексикографическое сравнение)
"Apple" < "apple"; // true (большие буквы < маленьких)
"10" < "2"; // true (как символы '1' < '2')

// Регистронезависимое сравнение
let str1 = "Hello";
let str2 = "hello";
str1.toLowerCase() === str2.toLowerCase(); // true
```

## 🎯 Практические примеры

### 🎮 Проверка возраста с категориями

```javascript
function ageCategory(age) {
  if (age < 0) return "некорректный возраст";
  if (age < 12) return "ребенок";
  if (age < 18) return "подросток";
  if (age < 65) return "взрослый";
  return "пожилой";
}

console.log(ageCategory(25)); // "взрослый"
console.log(ageCategory(8)); // "ребенок"
```

### 🛒 Расчет скидки

```javascript
function calculateDiscount(sum, isClubMember) {
  let discount = 0;

  // Много условий ИЛИ
  if (sum > 10000 || isClubMember) {
    discount = 10;
  }

  // Дополнительная скидка для постоянных клиентов
  if (sum > 10000 && isClubMember) {
    discount = 15; // Максимальная скидка
  }

  return discount;
}

console.log(`Скидка: ${calculateDiscount(15000, true)}%`); // 15%
console.log(`Скидка: ${calculateDiscount(5000, true)}%`); // 10%
console.log(`Скидка: ${calculateDiscount(15000, false)}%`); // 10%
```

### 🔐 Проверка пароля

```javascript
function validatePassword(password) {
  // Минимум 8 символов И содержит буквы И цифры
  let isLong = password.length >= 8;
  let hasLetters = /[a-zA-Z]/.test(password);
  let hasDigits = /[0-9]/.test(password);

  return isLong && hasLetters && hasDigits;
}

console.log(validatePassword("password123")); // true
console.log(validatePassword("123")); // false
console.log(validatePassword("пароль")); // false
```

### 📊 Статистика массива

```javascript
function statistics(numbers) {
  let sum = 0;
  let max = -Infinity;
  let min = Infinity;
  let even = 0;
  let odd = 0;

  for (let number of numbers) {
    sum += number;
    max = number > max ? number : max;
    min = number < min ? number : min;

    if (number % 2 === 0) {
      even++;
    } else {
      odd++;
    }
  }

  return {
    sum,
    average: sum / numbers.length,
    max,
    min,
    even,
    odd,
  };
}

let data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
console.log(statistics(data));
```

### 🎲 Генератор случайных чисел

```javascript
function randomRange(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

// Бросок кубика
let dice = randomRange(1, 6);
console.log(`Выпало: ${dice}`);

// Случайный выбор из массива
let fruits = ["яблоко", "банан", "апельсин"];
let randomFruit = fruits[randomRange(0, fruits.length - 1)];
console.log(`Случайный фрукт: ${randomFruit}`);
```

## 🚨 Частые ошибки новичков

### ❌ Путаница == и ===

```javascript
// ❌ ПЛОХО - неожиданное преобразование
if (user == "admin") {
  /* ... */
}

// ✅ ХОРОШО - строгое сравнение
if (user === "admin") {
  /* ... */
}
```

### ❌ Путаница = и ==

```javascript
let online = true;

// ❌ ПЛОХО - присваивание вместо сравнения
if ((online = false)) {
  /* не выполнится: результат присваивания равен false */
}

// ✅ ХОРОШО - сравнение
if (online === false) {
  /* ... */
}
```

### ❌ Деление строк

```javascript
let numA = "10";
let numB = "2";

console.log(numA / numB); // 5 (работает!)
console.log(numA * numB); // 20 (работает!)
console.log(numA - numB); // 8  (работает!)
console.log(numA + numB); // "102" (склеивание!) ❌
```

### ❌ Порядок операторов

```javascript
let result = 2 + 3 * 4; // 14 (сначала умножение)
let result2 = (2 + 3) * 4; // 20 (сначала сложение)
```

## 📚 Шпаргалка приоритета операторов

| Приоритет  | Операторы         | Направление |
| ---------- | ----------------- | ----------- |
| 1 (высший) | `()`              | →           |
| 2          | `**`              | ←           |
| 3          | `* / %`           | →           |
| 4          | `+ -`             | →           |
| 5          | `< <= > >=`       | →           |
| 6          | `== === != !==`   | →           |
| 7          | `&&`              | →           |
| 8          | `\|\|` | → |
| 9 (низший) | `=` `+= -= *= /=` | ←           |

## 📚 Шпаргалка быстрых операций

| Задача                 | Оператор | Пример    |
| ---------------------- | -------- | --------- |
| Сложение               | `+`      | `a + b`   |
| Вычитание              | `-`      | `a - b`   |
| Умножение              | `*`      | `a * b`   |
| Деление                | `/`      | `a / b`   |
| Остаток                | `%`      | `a % b`   |
| Степень                | `**`     | `a ** b`  |
| Увеличить на 1         | `++`     | `x++`     |
| Уменьшить на 1         | `--`     | `x--`     |
| Прибавить к переменной | `+=`     | `x += 5`  |
| Отнять от переменной   | `-=`     | `x -= 5`  |
| Строгое сравнение      | `===`    | `x === y` |
| Не строгое сравнение   | `==`     | `x == y`  |
| И (AND)                | `&&`     | `x && y`  |
| ИЛИ (OR) | `\|\|` | `x \|\| y` |
| НЕ (NOT)               | `!`      | `!x`      |

## 🎮 Практика в консоли

Открой F12 и попробуй:

```javascript
// Математика
let a = 10;
let b = 3;
console.log(`${a} + ${b} = ${a + b}`);
console.log(`${a} - ${b} = ${a - b}`);
console.log(`${a} * ${b} = ${a * b}`);
console.log(`${a} / ${b} = ${a / b}`);
console.log(`${a} % ${b} = ${a % b}`);

// Сравнения
console.log(`5 == "5": ${5 == "5"}`);
console.log(`5 === "5": ${5 === "5"}`);
console.log(`"apple" < "banana": ${"apple" < "banana"}`);

// Логика
let age = 20;
let student = true;
let canWork = age >= 18 && student;
console.log(`Может работать: ${canWork}`);

// Увеличение счетчика
let counter = 0;
for (let i = 0; i < 5; i++) {
  counter++;
  console.log(`Шаг ${counter}`);
}
```


## 📝 Задания для закрепления

### Задание 1: Вычисли результат
Определи значения без запуска кода:
```javascript
let a = 10;
let b = 3;
console.log(a % b);     // ?
console.log(a ** 2);     // ?
console.log(++a + b--);  // ?
console.log(a, b);       // ?
```

### Задание 2: Функция isEven
Напиши функцию `isEven(number)`, которая возвращает `true` если число чётное, и `false` если нечётное. Используй оператор `%`.

### Задание 3: Функция clamp
Напиши функцию `clamp(value, min, max)`, которая ограничивает значение в диапазоне. Если `value` меньше `min` — вернуть `min`, если больше `max` — вернуть `max`, иначе — `value`.
```javascript
clamp(5, 1, 10);  // 5
clamp(-3, 1, 10); // 1
clamp(15, 1, 10); // 10
```

### Задание 4: Калькулятор скидки
Напиши функцию `finalPrice(price, discount)`, где `discount` — процент скидки. Функция возвращает финальную цену. Если скидка больше 100% или меньше 0%, вернуть исходную цену.

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** Операторы - это как математические знаки для компьютера! Они позволяют считать, сравнивать и принимать решения. ⚡

Используй строгие операторы (`===`, `!==`) и будь внимателен с преобразованием типов! 🔍

---

[⬅️ Предыдущая тема: Типы данных](types-js.md) | [📚 Оглавление](README.md) | [Следующая тема: Условия ➡️](conditions-js.md)
