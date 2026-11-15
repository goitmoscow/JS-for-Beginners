# Объекты JavaScript 🏰

> **📚 Для кого этот материал:** Для тех, кто хочет научиться хранить связанные данные вместе.
>
> **🎯 Что ты узнаешь:** Что такое объекты, как создавать свойства, получать к ним доступ и работать со сложными структурами данных.
>
> **💡 Важно:** В примерах кода имена переменных написаны на английском языке (например: `name`, `age`, `user`). Это стандарт в программировании!

## 🎦 Что такое объект?

Представь объект как **контейнер с ящичками**:

🏰 **Контейнер** = сам объект
📦 **Ящичек** = свойство объекта
🏷️ **Этикетка на ящичке** = ключ свойства
💎 **Содержимое ящичка** = значение свойства

```javascript
let person = {
  name: "Анна", // ключ: "name", значение: "Анна"
  age: 28, // ключ: "age", значение: 28
  city: "Казань",
};
```

## 🏗️ Создание объектов

### 🎯 Способ 1: Литерал объекта (самый частый)

```javascript
// Пустой объект
let empty = {};

// С данными
let user = {
  name: "Михаил",
  age: 32,
  email: "mikhail@example.com",
};
```

### 🎯 Способ 2: Конструктор Object

```javascript
let book = new Object();
book.title = "Война и мир";
book.author = "Толстой";
book.year = 1869;
```

### 🎯 Способ 3: Фабричная функция

```javascript
function createUser(name, age) {
  return {
    name: name,
    age: age,
  };
}

let user1 = createUser("Ольга", 25);
let user2 = createUser("Дмитрий", 30);
```

## 🎯 Доступ к свойствам

### 📦 Точечная нотация (когда знаем имя свойства)

```javascript
let person = {
  name: "Елена",
  age: 27,
};

console.log(person.name); // "Елена"
person.age = 28; // Меняем значение
```

### 🔑 Квадратные скобки (когда имя в переменной)

```javascript
let person = {
  "user name": "Виктор", // В этом ключе действительно есть пробел
  email: "viktor@example.com",
};

// Для ключа с пробелом нужны квадратные скобки.
// person.username — допустимый синтаксис, но это другое свойство.
console.log(person["user name"]); // "Виктор"

let key = "email";
console.log(person[key]); // "viktor@example.com"

// Можно динамически создавать свойства
let newProperty = "phone";
person[newProperty] = "+7(999)123-45-67";
```

## 🔄 Изменение и добавление свойств

```javascript
let car = {
  brand: "Toyota",
  model: "Camry",
};

// ✍️ Добавляем новое свойство
car.year = 2020;
car["color"] = "синий";

// 📝 Изменяем существующее
car.model = "RAV4";

// 🗑️ Удаляем свойство
delete car.year;

console.log(car);
// { brand: "Toyota", model: "RAV4", color: "синий" }
```

## 🔍 Проверка существования свойств

```javascript
let student = {
  name: "Александр",
  course: 3,
};

// Способ 1: значение не undefined (не отличает отсутствие от значения undefined)
if (student.name !== undefined) {
  console.log("Имя есть");
}

// Способ 2: in — включает и унаследованные свойства
if ("age" in student) {
  console.log("Свойство возраст есть");
} else {
  console.log("Свойства возраст нет");
}

// Способ 3: Object.hasOwn — только собственные свойства, даже со значением undefined
if (Object.hasOwn(student, "name")) {
  console.log("Собственное свойство имя");
}
```

## 🎯 Типы данных в свойствах

Объект может хранить ЛЮБЫЕ типы данных:

```javascript
let complexObject = {
  // Простые типы
  number: 42,
  string: "привет",
  truth: true,

  // Сложные типы
  array: [1, 2, 3],
  nested: {
    name: "вложенный",
    value: 100,
  },

  // Функции
  method: function () {
    console.log("Я функция в объекте!");
  },

  // Другой объект
  ref: null,
};

// Доступ ко всему одинаково
console.log(complexObject.array[0]); // 1
console.log(complexObject.nested.name); // "вложенный"
complexObject.method(); // "Я функция в объекте!"
```

## 🔄 Обход свойств объекта

### 🏃 for...in (перечисляемые строковые свойства, включая унаследованные)

```javascript
let phone = {
  brand: "iPhone",
  model: "13",
  memory: "256GB",
};

for (let key in phone) {
  console.log(`${key}: ${phone[key]}`);
}
// brand: iPhone
// model: 13
// memory: 256GB
```

### 🔑 Object.keys() (свои перечисляемые строковые ключи)

```javascript
let student = {
  name: "Мария",
  age: 21,
  faculty: "Информатика",
};

let keys = Object.keys(student);
console.log(keys); // ["name", "age", "faculty"]

for (let key of keys) {
  console.log(`${key} = ${student[key]}`);
}
```

### 📋 Object.values() и Object.entries()

```javascript
let product = {
  title: "Ноутбук",
  price: 75000,
  quantity: 5,
};

// Только значения
let values = Object.values(product);
console.log(values); // ["Ноутбук", 75000, 5]

// Пары [ключ, значение]
let pairs = Object.entries(product);
console.log(pairs);
// [["title", "Ноутбук"], ["price", 75000], ["quantity", 5]]

for (let [key, value] of pairs) {
  console.log(`${key}: ${value}`);
}
```

## 🧹 Копирование объектов

### ❌ Простое присваивание (не копирует, а ссылается)

```javascript
let original = { name: "Петр", age: 35 };
let copy = original; // ❌ Это не копия!

copy.age = 36;
console.log(original.age); // 36 (изменился оригинал!)
```

### ✅ Поверхностное копирование Object.assign()

```javascript
let original = { name: "Игорь", age: 40 };
let copy = Object.assign({}, original);

copy.age = 41;
console.log(original.age); // 40 (оригинал не изменился!)
console.log(copy.age); // 41
```

### ✅ Современное копирование spread-оператором

```javascript
let original = { name: "Светлана", city: "Екатеринбург" };
let copy = { ...original };

copy.city = "Москва";
console.log(original.city); // "Екатеринбург"
console.log(copy.city); // "Москва"
```

### ⚠️ Глубокое копирование (для вложенных объектов)

```javascript
let complexOriginal = {
  name: "Антон",
  contacts: {
    phone: "+7(999)111-22-33",
    email: "anton@example.com",
  },
};

// Для поддерживаемых структур данных используйте structuredClone.
let deepCopy = structuredClone(complexOriginal);
// Функции не клонируются: для них будет DataCloneError.

deepCopy.contacts.phone = "+7(999)999-88-77";
console.log(complexOriginal.contacts.phone); // "+7(999)111-22-33"
console.log(deepCopy.contacts.phone); // "+7(999)999-88-77"
```

JSON.parse(JSON.stringify(value)) не является универсальным клонированием: теряет undefined, функции и Symbol, превращает Date в строку и не поддерживает BigInt и циклические ссылки. structuredClone поддерживает вложенные данные и циклы, но не функции и DOM-узлы.

## 🎯 Практические примеры

### 📱 Профиль пользователя

```javascript
let user = {
  personalInfo: {
    name: "Екатерина",
    lastName: "Волкова",
    age: 28,
  },
  contacts: {
    email: "ekaterina@example.com",
    phone: "+7(900)123-45-67",
  },
  settings: {
    theme: "темная",
    notifications: true,
  },
};

// Доступ к вложенным данным
console.log(
  `Пользователь: ${user.personalInfo.name} ${user.personalInfo.lastName}`,
);
console.log(`Email: ${user.contacts.email}`);

// Изменение настроек
user.settings.theme = "светлая";
user.settings.notifications = false;
```

### 🛒 Корзина покупок

```javascript
let cart = {
  items: [
    { title: "Молоко", price: 80, count: 2 },
    { title: "Хлеб", price: 45, count: 1 },
    { title: "Яблоки", price: 120, count: 0.5 },
  ],
  info: {
    delivery: false,
    address: null,
  },

  calculateSum: function () {
    let sum = 0;
    for (let item of this.items) {
      sum += item.price * item.count;
    }
    return sum;
  },
};

console.log(`Общая сумма: ${cart.calculateSum()} руб`);
// Общая сумма: 265 руб
```

## 🚨 Частые ошибки новичков

### ❌ Обращение к несуществующему свойству

```javascript
let person = { name: "Олег" };
console.log(person.age); // undefined (не ошибка, но неожиданно)
console.log(person.address.city); // ❌ TypeError! Cannot read property 'city' of undefined

// Решение: проверяйте вложенность
if (person.address && person.address.city) {
  console.log(person.address.city);
}
```

### ❌ Изменение const объекта

```javascript
const config = {
  lang: "русский",
  theme: "светлая",
};

config.lang = "английский"; // ✅ Можно! Меняем содержимое
config = {}; // ❌ Нельзя! Меняем саму ссылку
```

### ❌ Путаница между объектом и массивом

```javascript
let array = [1, 2, 3];
array.key = "значение"; // Технически можно, но ПЛОХАЯ ПРАКТИКА!

let object = { 0: "ноль", 1: "один" };
object.forEach((item) => console.log(item)); // ❌ Ошибка! У объектов нет forEach
```

## 📚 Шпаргалка быстрых операций

| Задача             | Код                                |
| ------------------ | ---------------------------------- |
| Создать объект     | `let obj = {};`                    |
| Добавить свойство  | `obj.key = value;`                 |
| Удалить свойство   | `delete obj.key;`                  |
| Проверить свойство | `'key' in obj;`                    |
| Получить ключи     | `Object.keys(obj);`                |
| Получить значения  | `Object.values(obj);`              |
| Копировать объект  | `let copy = {...obj};`             |
| Слить объекты      | `let merged = {...obj1, ...obj2};` |

## 🎮 Практика в консоли

Открой F12 и попробуй:

```javascript
// Создай свой профиль
let profile = {
  name: "Твое имя",
  age: 25,
  hobbies: ["программирование", "музыка"],
};

// Добавь новые данные
profile.city = "Твой город";
profile.mood = "отличное";

// Выведи всё
for (let [key, value] of Object.entries(profile)) {
  console.log(`${key}: ${value}`);
}

// Сделай копию и измени
let copy = { ...profile };
copy.age = 26;

console.log("Оригинал:", profile);
console.log("Копия:", copy);
```

## 📝 Задания для закрепления

### Задание 1: Объект-автомобиль
Создай объект `car` со свойствами: марка, модель, год, цвет, пробег. Добавь метод `getInfo()`, который возвращает строку вида: "Toyota Camry 2020, цвет: синий, пробег: 45000 км".

### Задание 2: Объединение объектов
Напиши функцию `mergeObjects(obj1, obj2)`, которая возвращает новый объект с ключами обоих. При совпадении ключей значения из `obj2` перезаписывают значения из `obj1`.
```javascript
mergeObjects({ a: 1, b: 2 }, { b: 3, c: 4 }); // { a: 1, b: 3, c: 4 }
```

### Задание 3: Выбрать ключи
Напиши функцию `pick(obj, keys)`, которая возвращает новый объект только с указанными собственными ключами. Отсутствующие ключи пропускай; существующие со значением undefined сохраняй.
```javascript
const user = { name: "Анна", age: 25, email: "a@b.com", city: "Москва" };
pick(user, ["name", "email"]); // { name: "Анна", email: "a@b.com" }
```

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** Объекты - это как ящик с органайзером для хранения связанных данных! 🏰

Организуй данные логически, и твой код станет чище и понятнее! 🧹

---

[⬅️ Предыдущая тема: Массивы](arrays-js.md) | [📚 Оглавление](README.md) | [Следующая тема: Функции (продвинутые) ➡️](advanced-functions.md)
