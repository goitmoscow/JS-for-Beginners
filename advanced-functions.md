# Функции - продвинутые концепции 🎯

> **📚 Для кого этот материал:** Для тех, кто уже знаком с базовыми функциями и хочет углубить знания.
>
> **🎯 Что ты узнаешь:** Стрелочные функции, замыкания, области видимости, IIFE и каррирование.
>
> **💡 Важно:** В примерах кода имена переменных написаны на английском языке (например: `name`, `age`, `user`). Это стандарт в программировании!

## 🎦 Что такое продвинутые функции?

Представь обычные функции как **простые рецепты**, а продвинутые - как **кулинарные техники шеф-повара**:

📝 **Простая функция** = добавить 2 + 3  
🎯 **Стрелочная функция** = короткая запись "2+3"  
🔒 **Замыкание** = секретный ингредиент, который запоминается  
🎭 **Область видимости** = кухня, где работают только определенные инструменты

## ⚡ Стрелочные функции (Arrow Functions)

### 🎯 Базовый синтаксис

```javascript
// Обычная функция
function add(a, b) {
  return a + b;
}

// Стрелочная функция
const addArrow = (a, b) => a + b;
console.log(add(2, 3), addArrow(2, 3)); // 5 5
```

### 🎯 Разные формы стрелочных функций

```javascript
// 1. Без параметров
const hello = () => "Привет мир!";

// 2. Один параметр (скобки можно опустить)
const square = (x) => x * x;

// 3. Несколько параметров (скобки обязательны)
const sum = (a, b, c) => a + b + c;

// 4. Многострочная функция (фигурные скобки и return обязательны)
const info = (name, age) => {
  let birthYear = new Date().getFullYear() - age;
  return `${name}, ${age} лет (родился в ${birthYear})`;
};
```

### 🔄 Отличия от обычных функций

```javascript
// ❌ Обычная функция - свой this
const object = {
  name: "Анна",
  showRegular: function () {
    setTimeout(function () {
      console.log(this.name); // В браузере this = window, не object; значение зависит от window.name
    }, 1000);
  },
};

// ✅ Стрелочная функция - наследует this
const object2 = {
  name: "Борис",
  showArrow: function () {
    setTimeout(() => {
      console.log(this.name); // "Борис" (this сохранен)
    }, 1000);
  },
};
```

### 🎯 Практическое применение

```javascript
let numbers = [1, 2, 3, 4, 5];

// Обычная функция в map
let doubled = numbers.map(function (number) {
  return number * 2;
});

// Стрелочная функция (короче!)
let doubled2 = numbers.map((number) => number * 2);

// В filter
let even = numbers.filter((number) => number % 2 === 0);

// В reduce
let sum = numbers.reduce((accumulator, number) => accumulator + number, 0);
```

## 🔒 Замыкания (Closures)

### 🎦 Что такое замыкание?

Представь **фабрику с секретом**:

🏭 **Фабрика** = внешняя функция  
🔐 **Секрет** = переменная внутри фабрики  
📦 **Продукт** = внутренняя функция, которая знает секрет

```javascript
function createCounter() {
  let counter = 0; // Секретная переменная

  // Внутренняя функция "знает" про счетчик
  return function () {
    counter++;
    return counter;
  };
}

const myCounter = createCounter();
console.log(myCounter()); // 1
console.log(myCounter()); // 2
console.log(myCounter()); // 3

const anotherCounter = createCounter();
console.log(anotherCounter()); // 1 (независимый счетчик!)
```

### 🎯 Практические примеры замыканий

#### 💾 Карман для данных

```javascript
function createUser(name) {
  let age = 0; // Приватная переменная

  return {
    setAge: function (newAge) {
      age = newAge;
    },
    getAge: function () {
      return age;
    },
    greet: function () {
      return `${name}, тебе ${age} лет`;
    },
  };
}

const anna = createUser("Анна");
anna.setAge(25);
console.log(anna.greet()); // "Анна, тебе 25 лет"

// anna.age // undefined - приватная переменная недоступна!
```

#### 🏭 Фабрика функций

```javascript
function createMultiplier(multiplier) {
  return function (number) {
    return number * multiplier;
  };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5)); // 10
console.log(triple(5)); // 15

// Это как калькулятор с настроенной кнопкой!
```

#### 🎨 Генератор уникальных ID

```javascript
function createIdGenerator() {
  let lastId = 0;

  return function () {
    lastId++;
    return `ID_${lastId}`;
  };
}

const generator = createIdGenerator();

console.log(generator()); // ID_1
console.log(generator()); // ID_2
console.log(generator()); // ID_3
```

## 🏛️ Области видимости (Scope)

### 🎦 Что такое область видимости?

Представь **дом с комнатами**:

🏠 **Глобальная область** = улица (доступно всем)  
🏡 **Функциональная область** = дом (доступно внутри дома)  
🚪 **Блочная область** = комната (доступно только в комнате)

### 🌍 Глобальная область видимости

```javascript
let globalVariable = "Я доступен везде!";

function func() {
  console.log(globalVariable); // ✅ Видно
}

func();
console.log(globalVariable); // ✅ Видно

// ⚠️ Избегай глобальных переменных!
```

### 🏡 Функциональная область видимости

```javascript
function createRoom() {
  let furniture = "стол"; // Видно только внутри функции

  console.log(furniture); // ✅ Видно
}

createRoom();
// console.log(furniture); // ❌ Ошибка! furniture не определена
```

### 🚪 Блочная область видимости (let/const)

```javascript
if (true) {
  let blockVariable = "Я в блоке!";
  const constant = "Тоже в блоке!";

  console.log(blockVariable); // ✅ Видно
}

// console.log(blockVariable); // ❌ Ошибка!
// console.log(constant); // ❌ Ошибка!

// С var работало бы по-другому (плохо!)
if (true) {
  var oldVariable = "Я утеку из блока!";
}
console.log(oldVariable); // ✅ Работает (но это плохо!)
```

### 🔍 Цепочка областей видимости

```javascript
let level1 = "глобальный";

function outer() {
  let level2 = "внешняя функция";

  function inner() {
    let level3 = "внутренняя функция";

    console.log(level3); // Свои переменные
    console.log(level2); // Переменные родителя
    console.log(level1); // Глобальные переменные
  }

  inner();
  // console.log(level3); // ❌ Ошибка!
}

outer();
```

## 🎭 IIFE (Immediately Invoked Function Expression)

### 🎦 Что такое IIFE?

Представь **одноразовый рецепт**, который готовится и съедается сразу:

📝 **Рецепт** = функция  
👨‍🍳 **Приготовление** = вызов функции  
🍽️ **Сразу съесть** = результат готов сразу

```javascript
// Базовый синтаксис
(function () {
  console.log("Я выполняюсь сразу!");
})();

// С параметрами
(function (name) {
  console.log(`Привет, ${name}!`);
})("Мир");

// Со стрелочной функцией
(() => {
  console.log("Я стрелочная IIFE!");
})();
```

### 🎯 Практическое применение IIFE

#### 🔒 Изоляция кода

```javascript
(function () {
  let privateVariable = "секрет";

  function secretFunction() {
    return "Только для внутреннего использования";
  }

  // Ничего не "утекает" в глобальную область
})();

// privateVariable // ❌ Ошибка!
// secretFunction()    // ❌ Ошибка!
```

#### 🏭 Модульный паттерн

```javascript
const calculator = (function () {
  // Приватные переменные и функции
  let history = [];

  function addToHistory(operation, result) {
    history.push(`${operation} = ${result}`);
  }

  // Публичный интерфейс
  return {
    add: function (a, b) {
      let result = a + b;
      addToHistory(`${a} + ${b}`, result);
      return result;
    },

    subtract: function (a, b) {
      let result = a - b;
      addToHistory(`${a} - ${b}`, result);
      return result;
    },

    getHistory: function () {
      return [...history]; // Возвращаем копию
    },
  };
})();

calculator.add(5, 3); // 8
calculator.subtract(10, 4); // 6
console.log(calculator.getHistory()); // ["5 + 3 = 8", "10 - 4 = 6"]
```

## 🔄 Каррирование (Currying)

### 🎦 Что такое каррирование?

Представь **конструктор с последовательными настройками**:

🔧 **Шаг 1** = выбрать тип инструмента  
🔧 **Шаг 2** = выбрать размер  
🔧 **Шаг 3** = выбрать материал  
🎯 **Результат** = готовый инструмент

```javascript
function add(a) {
  return function (b) {
    return function (c) {
      return a + b + c;
    };
  };
}

console.log(add(1)(2)(3)); // 6

// Или шаг за шагом
const step1 = add(1);
const step2 = step1(2);
const result = step2(3);
console.log(result); // 6
```

### 🎯 Практическое применение каррирования

#### 📝 Генератор форматирования

```javascript
function format(type) {
  return function (separator) {
    return function (data) {
      return data.join(separator);
    };
  };
}

const withComma = format("csv")(",");
const withSemicolon = format("csv")(";");

const numbers = [1, 2, 3, 4];
console.log(withComma(numbers)); // "1,2,3,4"
console.log(withSemicolon(numbers)); // "1;2;3;4"
```

#### 🏪 Логирование с уровнями

```javascript
function createLogger(level) {
  return function (prefix) {
    return function (message) {
      console.log(`[${level}] ${prefix}: ${message}`);
    };
  };
}

const infoLog = createLogger("INFO");
const errorLog = createLogger("ERROR");

const infoUser = infoLog("Пользователь");
const errorSystem = errorLog("Система");

infoUser("Вошел в систему");
errorSystem("Ошибка базы данных");

// Вывод:
// [INFO] Пользователь: Вошел в систему
// [ERROR] Система: Ошибка базы данных
```

## 🎯 Практические примеры

### 🛒 Корзина покупок с замыканием

```javascript
function createCart() {
  let items = [];
  let totalPrice = 0;

  return {
    add: function (name, price, quantity = 1) {
      items.push({ name, price, quantity });
      totalPrice += price * quantity;
      console.log(`Добавлено: ${name} x${quantity}`);
    },

    remove: function (index) {
      if (index >= 0 && index < items.length) {
        let item = items[index];
        totalPrice -= item.price * item.quantity;
        items.splice(index, 1);
        console.log(`Удалено: ${item.name}`);
      }
    },

    getSummary: function () {
      return {
        items: items.map((item) => ({ ...item })), // Копируем и сами записи
        totalSum: totalPrice,
        itemCount: items.reduce(
          (sum, item) => sum + item.quantity,
          0,
        ),
      };
    },

    clear: function () {
      items = [];
      totalPrice = 0;
      console.log("Корзина очищена");
    },
  };
}

const myCart = createCart();
myCart.add("Молоко", 80, 2);
myCart.add("Хлеб", 45);
console.log(myCart.getSummary());
myCart.clear();
```

### 🎮 Игровой счетчик

```javascript
function createGameCounter() {
  let score = 0;
  let level = 1;
  let life = 3;

  return {
    addScore: function (points) {
      score += points;
      while (score >= level * 100) {
        level++;
        life++;
        console.log(`🎉 Новый уровень: ${level}, Жизни: ${life}`);
      }
      return score;
    },

    loseLife: function () {
      life--;
      console.log(`💔 Осталось жизней: ${life}`);
      if (life <= 0) {
        console.log("💀 Игра окончена!");
        return false;
      }
      return true;
    },

    getStatus: function () {
      return { score, level, life };
    },
  };
}

const game = createGameCounter();
game.addScore(50);
game.addScore(60); // Новый уровень!
game.loseLife();
console.log(game.getStatus());
```

### 🎨 Создание компонентов (простой React-паттерн)

```javascript
function createComponent(name) {
  let state = {};
  let element = null;

  return {
    render: function (container) {
      element = document.createElement("div");
      const heading = document.createElement("h1");
      heading.textContent = name;
      element.replaceChildren(heading);
      container.appendChild(element);
      return element;
    },

    setState: function (newState) {
      state = { ...state, ...newState };
      if (element) {
        element.querySelector("h1").textContent = `${name} - ${JSON.stringify(state)}`;
      }
    },

    getState: function () {
      return { ...state }; // Копия!
    },
  };
}

const button = createComponent("Кнопка");
button.render(document.body);
button.setState({ pressed: true, count: 5 });
```

## 🚨 Частые ошибки новичков

### ❌ Неправильное использование this в стрелочных функциях

```javascript
const object = {
  value: 10,

  // ❌ ПЛОХО - стрелочная функция не имеет своего this
  show: () => {
    console.log(this.value); // this взят снаружи: значение зависит от среды; в модуле возможен TypeError
  },

  // ✅ ХОРОШО - обычная функция
  showCorrect: function () {
    console.log(this.value); // 10
  },
};
```

### ❌ Утечка переменных из замыкания

```javascript
function createProblemClosure() {
  let counter = 0;
  let array = [];

  // ❌ С var - все функции будут использовать последнее значение i
  for (var i = 0; i < 5; i++) {
    setTimeout(() => {
      console.log(i); // 5, 5, 5, 5, 5
    }, i * 100);
  }

  // ✅ С let - блочная область видимости, каждая итерация имеет свою переменную
  for (let j = 0; j < 5; j++) {
    setTimeout(() => {
      console.log(j); // 0, 1, 2, 3, 4
    }, j * 100);
  }
}
```

### ❌ Изменение внешних переменных

```javascript
let globalVariable = 0;

function problem() {
  globalVariable = 100; // ❌ Изменяет внешнюю переменную
  console.log(globalVariable);
}

problem();
console.log(globalVariable); // 100 (изменилось извне)
```

## 📚 Шпаргалка быстрых концепций

| Концепция              | Когда использовать          | Пример                                   |
| ---------------------- | --------------------------- | ---------------------------------------- |
| **Стрелочные функции** | Короткие callback функции   | `arr.map(x => x * 2)`                    |
| **Замыкания**          | Приватные данные, состояние | `function(){ let x=0; return ()=>x++; }` |
| **IIFE**               | Изоляция кода, модули       | `(function(){ ... })()`                  |
| **Каррирование**       | Конфигурируемые функции     | `log(level)(prefix)(message)`            |
| **Блочная область**    | let/const для безопасности  | `if(true){ let x=1; }`                   |

## 🎮 Практика в консоли

Открой F12 и попробуй:

```javascript
// 1. Стрелочные функции
let numbers = [1, 2, 3, 4, 5];
let squares = numbers.map((x) => x * x);
console.log("Квадраты:", squares);

// 2. Замыкание
function createMemo() {
  let memory = [];
  return function (value) {
    if (arguments.length > 0) memory.push(value);
    return memory.slice(); // возвращаем копию
  };
}
const memo = createMemo();
memo("первое");
memo("второе");
console.log(memo());

// 3. IIFE
const result = (function (a, b) {
  return a * b + (a + b);
})(3, 4);
console.log("Результат IIFE:", result);

// 4. Каррирование
function logger(level) {
  return function (message) {
    return `[${level}] ${message}`;
  };
}
const warn = logger("WARN");
console.log(warn("Внимание!"));

// 5. Области видимости
let global = "глобально";
function test() {
  let local = "локально";
  console.log(global); // видно
  console.log(local); // видно
}
test();
// console.log(local); // ошибка!
```

## 📝 Задания для закрепления

### Задание 1: Стрелочные функции
Перепиши каждую функцию в стрелочную (максимально короткую форму):
```javascript
function double(x) { return x * 2; }
function isPositive(x) { return x > 0; }
function getFullName(first, last) { return first + " " + last; }
```

### Задание 2: Счётчик на замыкании
Создай функцию `createCounter(start)`, которая возвращает объект с тремя методами:
- `increment()` — увеличивает счётчик на 1
- `decrement()` — уменьшает на 1
- `getValue()` — возвращает текущее значение

```javascript
const counter = createCounter(10);
counter.increment();
counter.increment();
counter.decrement();
counter.getValue(); // 11
```

### Задание 3: Функция once
Создай функцию `once(fn)`, которая позволяет вызвать переданную функцию только один раз. Повторные вызовы возвращают результат первого.
```javascript
const initialize = once(() => {
  console.log("Инициализация!");
  return 42;
});

initialize(); // "Инициализация!", вернёт 42
initialize(); // ничего не выведет, вернёт 42
```

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** Продвинутые функции - это как профессиональные инструменты! Они позволяют создавать более гибкий и безопасный код. 🛠️

Используй стрелочные функции для краткости, замыкания для приватных данных, и не забывай про области видимости! 🎯

---

[⬅️ Предыдущая тема: Объекты](objects-js.md) | [📚 Оглавление](README.md) | [Следующая тема: Асинхронность ➡️](async-js.md)
