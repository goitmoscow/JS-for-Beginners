# Массивы JavaScript 📋

> **📚 Для кого этот материал:** Для тех, кто хочет научиться работать со списками данных.
>
> **🎯 Что ты узнаешь:** Как создавать массивы, добавлять и удалять элементы, искать значения и использовать методы массивов.
>
> **💡 Важно:** В примерах кода имена переменных написаны на английском языке (например: `name`, `age`, `user`). Это стандарт в программировании!

## 🎦 Что такое массив?

Представь массив как **полку с пронумерованными ячейками**:

📋 **Полка** = сам массив  
📦 **Ячейки** = элементы массива  
🔢 **Номера ячеек** = индексы (начиная с 0!)

```javascript
let fruits = ["яблоко", "банан", "апельсин"];
//               0         1          2
```

## 🏗️ Создание массивов

### 🎯 Способ 1: Литерал массива (самый частый)

```javascript
// Пустой массив
let empty = [];

// С данными
let numbers = [1, 2, 3, 4, 5];
let mixed = ["текст", 42, true, null, { key: "значение" }];
```

### 🎯 Способ 2: Конструктор Array

```javascript
let empty2 = new Array();
let withSize = new Array(5); // [empty × 5] - 5 пустых ячеек
let withElements = new Array(1, 2, 3); // [1, 2, 3]
```

### 🎯 Способ 3: Array.of()

```javascript
let array = Array.of(10); // [10] - один элемент 10
let several = Array.of(1, 2, 3); // [1, 2, 3]
```

## 🔍 Доступ к элементам

```javascript
let colors = ["красный", "зеленый", "синий"];

// Доступ по индексу (начинается с 0!)
console.log(colors[0]); // "красный"
console.log(colors[1]); // "зеленый"
console.log(colors[2]); // "синий"

// Изменение элемента
colors[1] = "желтый";
console.log(colors); // ["красный", "желтый", "синий"]

// Добавление в конец
colors[3] = "фиолетовый";
console.log(colors); // ["красный", "желтый", "синий", "фиолетовый"]
```

## 📏 Основные свойства

### 📐 Длина массива

```javascript
let items = [10, 20, 30, 40, 50];
console.log(items.length); // 5

// Последний элемент (частый паттерн)
console.log(items[items.length - 1]); // 50

// Динамическая длина
items.push(60);
console.log(items.length); // 6
```

## 🔄 Основные методы массивов

### ➕ Добавление элементов

```javascript
let list = ["пункт1", "пункт2"];

// push() - добавить в конец
list.push("пункт3");
list.push("пункт4", "пункт5"); // несколько сразу
console.log(list); // ["пункт1", "пункт2", "пункт3", "пункт4", "пункт5"]

// unshift() - добавить в начало
list.unshift("пункт0");
console.log(list); // ["пункт0", "пункт1", "пункт2", "пункт3", "пункт4", "пункт5"]
```

### ➖ Удаление элементов

```javascript
let numbers = [10, 20, 30, 40, 50];

// pop() - удалить и вернуть последний
let last = numbers.pop(); // 50
console.log(numbers); // [10, 20, 30, 40]

// shift() - удалить и вернуть первый
let first = numbers.shift(); // 10
console.log(numbers); // [20, 30, 40]

// splice() - удалить по индексу (самый мощный)
numbers.splice(1, 1); // удалить 1 элемент начиная с индекса 1
console.log(numbers); // [20, 40]

// splice() с заменой
numbers.splice(0, 1, 99); // удалить 1 элемент с индекса 0, вставить 99
console.log(numbers); // [99, 40]
```

### 🔍 Поиск в массиве

```javascript
let users = ["Анна", "Борис", "Виктор", "Галина"];

// indexOf() - найти индекс элемента
let borisIndex = users.indexOf("Борис"); // 1
let unknownIndex = users.indexOf("Зинаида"); // -1 (не найден)

// includes() - проверить наличие элемента
console.log(users.includes("Виктор")); // true
console.log(users.includes("Зинаида")); // false

// find() - найти элемент по условию
let numbers = [1, 5, 10, 15, 20];
let greaterThanTen = numbers.find((number) => number > 10); // 15 (первый найденный)
let lessThanZero = numbers.find((number) => number < 0); // undefined (не найден)
```

### 🔧 Модификация массива

```javascript
let arr = [1, 2, 3, 4, 5];

// map() - создать новый массив с преобразованием
let doubled = arr.map((x) => x * 2); // [2, 4, 6, 8, 10]
let strings = arr.map((x) => `число: ${x}`); // ["число: 1", "число: 2", ...]

// filter() - создать новый массив с фильтрацией
let even = arr.filter((x) => x % 2 === 0); // [2, 4]
let greaterThanThree = arr.filter((x) => x > 3); // [4, 5]

// sort() - сортировка (опасно для чисел!)
let fruits = ["банан", "яблоко", "апельсин"];
fruits.sort(); // ["апельсин", "банан", "яблоко"]

let numbers = [3, 1, 10, 2];
numbers.sort(); // [1, 10, 2, 3] ❌ лексическая сортировка!

// Правильная сортировка чисел
numbers.sort((a, b) => a - b); // [1, 2, 3, 10]
numbers.sort((a, b) => b - a); // [10, 3, 2, 1] по убыванию
```

### 🔗 Объединение массивов

```javascript
let array1 = [1, 2, 3];
let array2 = [4, 5, 6];

// concat() - объединить
let combined = array1.concat(array2); // [1, 2, 3, 4, 5, 6]

// Spread оператор (современный способ)
let combined2 = [...array1, ...array2]; // [1, 2, 3, 4, 5, 6]
let mixed = [0, ...array1, 99, ...array2, 100]; // [0, 1, 2, 3, 99, 4, 5, 6, 100]
```

map/filter/slice создают поверхностные копии: объекты внутри могут оставаться общими. sort, reverse, splice, push и pop меняют исходный массив. Если нужна сортировка копии, используйте toSorted((a, b) => a - b) или slice().sort((a, b) => a - b).

## 🏃 Обход массивов

### 🔄 forEach() - выполнить действие для каждого элемента

```javascript
let fruits = ["яблоко", "банан", "апельсин"];

// Классический вариант
fruits.forEach(function (fruit, index, array) {
  console.log(`${index}: ${fruit}`);
});

// Современный вариант со стрелочной функцией
fruits.forEach((fruit, index) => {
  console.log(`${index}: ${fruit}`);
});
```

### 🎯 for...of - современный цикл

```javascript
let numbers = [10, 20, 30];

for (let number of numbers) {
  console.log(number);
}
// 10
// 20
// 30

for (let [index, number] of numbers.entries()) {
  console.log(`${index}: ${number}`);
}
```

### 🔧 Пример с условием

```javascript
let grades = [5, 3, 4, 5, 2, 5];

let excellent = [];
grades.forEach((grade) => {
  if (grade === 5) {
    excellent.push(grade);
  }
});

console.log(`Отличных оценок: ${excellent.length}`); // 3
```

## 🧮 Агрегирующие методы

### 🔢 reduce() - сворачивание массива в одно значение

```javascript
let numbers = [1, 2, 3, 4, 5];

// Сумма всех чисел
let sum = numbers.reduce((accumulator, number) => accumulator + number, 0);
console.log(sum); // 15

// Произведение всех чисел
let product = numbers.reduce((accumulator, number) => accumulator * number, 1);
console.log(product); // 120

// Поиск максимального
let maximum = numbers.reduce((max, number) => (max > number ? max : number));
console.log(maximum); // 5
```

Без начального значения reduce выбросит TypeError на пустом массиве. Для суммы укажите 0, для произведения — 1; максимум пустого набора требует отдельного соглашения.

### ✅ every() и some() - проверки

```javascript
let numbers = [2, 4, 6, 8];

// every() - все ли соответствуют условию?
let allEven = numbers.every((number) => number % 2 === 0); // true
let allGreaterThan5 = numbers.every((number) => number > 5); // false

// some() - есть ли хотя бы один?
let hasGreaterThan5 = numbers.some((number) => number > 5); // true
let hasOdd = numbers.some((number) => number % 2 !== 0); // false
```

На пустом массиве some возвращает false, every — true. forEach возвращает undefined; return внутри callback не завершает внешнюю функцию.

## 🎯 Практические примеры

### 🛒 Корзина товаров

```javascript
let cart = [
  { title: "Молоко", price: 80, quantity: 2 },
  { title: "Хлеб", price: 45, quantity: 1 },
  { title: "Яблоки", price: 120, quantity: 0.5 },
];

// Отфильтровать товары со скидкой
let discountedItems = cart.filter((item) => item.price < 100);
console.log(discountedItems);
// [{ title: "Молоко", price: 80, quantity: 2 }, { title: "Хлеб", price: 45, quantity: 1 }]

// Посчитать общую стоимость
let totalPrice = cart.reduce(
  (sum, item) => sum + item.price * item.quantity,
  0,
);
console.log(`Общая стоимость: ${totalPrice} руб`); // 265

// Получить названия товаров
let names = cart.map((item) => item.title);
console.log(names); // ["Молоко", "Хлеб", "Яблоки"]
```

### 📊 Анализ данных

```javascript
let studentGrades = [5, 4, 3, 5, 5, 3, 4, 4, 5, 2];

// Статистика
let average =
  studentGrades.reduce((sum, grade) => sum + grade, 0) /
  studentGrades.length;
console.log(`Средняя оценка: ${average.toFixed(2)}`); // 4.00

let maximum = Math.max(...studentGrades);
let minimum = Math.min(...studentGrades);
console.log(`Диапазон: ${minimum} - ${maximum}`); // 2 - 5

// Частотный анализ
let frequency = {};
studentGrades.forEach((grade) => {
  frequency[grade] = (frequency[grade] || 0) + 1;
});
console.log(frequency); // {2: 1, 3: 2, 4: 3, 5: 4}
```

### 🔄 Преобразование данных

```javascript
let users = [
  { id: 1, name: "Анна", age: 25 },
  { id: 2, name: "Борис", age: 30 },
  { id: 3, name: "Виктор", age: 35 },
];

// Получить только совершеннолетних
let adults = users
  .filter((person) => person.age >= 18)
  .map((person) => `${person.name} (${person.age} лет)`);

console.log(adults);
// ["Анна (25 лет)", "Борис (30 лет)", "Виктор (35 лет)"]
```

## 🚨 Частые ошибки новичков

### ❌ Доступ к несуществующему индексу

```javascript
let arr = [1, 2, 3];
console.log(arr[10]); // undefined (не ошибка!)
console.log(arr[10].someProperty); // ❌ TypeError! Cannot read property 'someProperty' of undefined

// Решение: проверяйте длину
if (arr.length > 10) {
  console.log(arr[10].someProperty);
}
```

### ❌ Изменение массива при обходе

```javascript
let numbers = [1, 2, 3, 4, 5];

// ❌ ПЛОХО - изменяем массив при обходе
numbers.forEach((number, index) => {
  if (number % 2 === 0) {
    numbers.splice(index, 1); // Нарушает индексацию!
  }
});

// ✅ ХОРОШО - создаем новый массив
let odd = numbers.filter((number) => number % 2 !== 0);
```

### ❌ Сортировка чисел

```javascript
let numbers = [1, 10, 2, 20];
numbers.sort(); // ❌ [1, 10, 2, 20] - строки, а не числа!

// ✅ ПРАВИЛЬНО
numbers.sort((a, b) => a - b); // [1, 2, 10, 20]
```

## 📚 Шпаргалка быстрых операций

| Задача            | Метод                | Пример                             |
| ----------------- | -------------------- | ---------------------------------- |
| Добавить в конец  | `push()`             | `arr.push(элемент)`                |
| Добавить в начало | `unshift()`          | `arr.unshift(элемент)`             |
| Удалить с конца   | `pop()`              | `arr.pop()`                        |
| Удалить с начала  | `shift()`            | `arr.shift()`                      |
| Найти индекс      | `indexOf()`          | `arr.indexOf(элемент)`             |
| Проверить наличие | `includes()`         | `arr.includes(элемент)`            |
| Фильтровать       | `filter()`           | `arr.filter(x => x > 0)`           |
| Преобразовать     | `map()`              | `arr.map(x => x * 2)`              |
| Отсортировать     | `sort((a,b) => a-b)` | `arr.sort((a,b) => a-b)`           |
| Объединить        | `[...arr1, ...arr2]` | `let merged = [...arr1, ...arr2]`  |
| Обойти все        | `forEach()`          | `arr.forEach(x => console.log(x))` |

## 🎮 Практика в консоли

Открой F12 и попробуй:

```javascript
// Создай массив товаров
let products = ["телевизор", "телефон", "ноутбук", "планшет"];

// Добавь элементы
products.push("часы", "наушники");

// Найди индекс ноутбука
let index = products.indexOf("ноутбук");
console.log(`Ноутбук на позиции: ${index}`);

// Отфильтруй короткие названия
let short = products.filter((product) => product.length <= 6);
console.log("Короткие названия:", short);

// Создай массив объектов
let items = [
  { name: "Молоко", price: 80 },
  { name: "Хлеб", price: 45 },
  { name: "Сыр", price: 250 },
];

// Посчитай среднюю цену
let averagePrice =
  items.reduce((sum, item) => sum + item.price, 0) /
  items.length;
console.log(`Средняя цена: ${averagePrice.toFixed(2)} руб`);
```


## 📝 Задания для закрепления

### Задание 1: Уникальные элементы
Напиши функцию `unique(array)`, которая возвращает новый массив без дубликатов.
```javascript
unique([1, 2, 2, 3, 3, 3, 4]); // [1, 2, 3, 4]
unique(["a", "b", "a", "c"]);  // ["a", "b", "c"]
```

### Задание 2: Работа со студентами
Дан массив студентов. Выполни три задачи:
```javascript
const students = [
  { name: "Анна", grade: 5 },
  { name: "Борис", grade: 3 },
  { name: "Виктор", grade: 4 },
  { name: "Галина", grade: 5 },
  { name: "Дмитрий", grade: 2 },
];
```
1. Найди среднюю оценку всех студентов
2. Получи массив имён отличников (оценка 5)
3. Отсортируй студентов по оценке (от лучшей к худшей)

### Задание 3: Разбить на группы
Напиши функцию `chunk(array, size)`, которая разбивает массив на подмассивы заданного размера. size должен быть положительным целым; иначе выброси RangeError. Пустой массив даёт [].
```javascript
chunk([1, 2, 3, 4, 5], 2);    // [[1, 2], [3, 4], [5]]
chunk([1, 2, 3, 4, 5, 6], 3); // [[1, 2, 3], [4, 5, 6]]
```

### Задание 4: Плоский массив
Напиши функцию `flatten(array)`, которая «расплющивает» вложенные массивы в один уровень.
```javascript
flatten([1, [2, [3, 4]], 5]); // [1, 2, 3, 4, 5]
flatten([[1, 2], [3, [4]]]); // [1, 2, 3, 4]
```

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** Массивы - это как пронумерованные полки, где каждый предмет имеет свой номер! 📋

Используй методы массивов, и твой код станет чистым и эффективным! 🚀

---

[⬅️ Предыдущая тема: Строки](strings-js.md) | [📚 Оглавление](README.md) | [Следующая тема: Объекты ➡️](objects-js.md)
