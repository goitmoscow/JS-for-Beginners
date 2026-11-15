# Строки JavaScript 📝

> **📚 Для кого этот материал:** Для тех, кто изучает работу с текстом в JavaScript.
>
> **🎯 Что ты узнаешь:** Как создавать строки, объединять их, искать подстроки и использовать методы строк.
>
> **💡 Важно:** В примерах кода имена переменных написаны на английском языке (например: `name`, `age`, `user`). Это стандарт в программировании!

## 🎦 Что такое строка?

Представь строку как **цепочку букв и символов**:

🔗 **Цепочка** = сама строка  
⚪ **Бусинки** = отдельные символы  
📍 **Позиция** = индекс символа (начиная с 0!)

```javascript
let word = "Привет";
//            012345 - индексы символов
```

## 🔤 Создание строк

### 🎯 Одинарные и двойные кавычки

```javascript
let text1 = "Привет мир!";
let text2 = 'Я тоже строка';

// Кавычки внутри кавычек
let quote = "Он сказал: 'Привет!'";
let anotherQuote = 'Она ответила: "И тебе привет!"';
```

### 🎯 Обратные кавычки (template strings) - САМЫЕ МОЩНЫЕ!

```javascript
let name = "Александр";
let age = 28;

// Обратные кавычки позволяют вставлять переменные
let greeting = `Привет, ${name}! Тебе ${age} лет.`;
console.log(greeting); // "Привет, Александр! Тебе 28 лет."

// Многострочные строки
let poem = `
Розовый слон
Пошел гулять по крыше.
Солнце светит ярко!
`;
console.log(poem);
```

## 📏 Свойства строк

### 📐 Длина строки

```javascript
let word = "JavaScript";
console.log(word.length); // 10

// Пробелы тоже считаются!
let phrase = "Привет мир!";
console.log(phrase.length); // 11 (пробел + восклицательный знак)

// Unicode символы
let emoji = "😀";
console.log(emoji.length); // 2 кодовые единицы UTF-16, хотя видимый символ один
```

## 🔍 Доступ к символам

```javascript
let text = "Программирование";

// Способ 1: через индекс
console.log(text[0]); // "П"
console.log(text[5]); // "а"

// Способ 2: метод charAt()
console.log(text.charAt(0)); // "П"
console.log(text.charAt(5)); // "а"

// Разница: выход за пределы
console.log(text[100]); // undefined
console.log(text.charAt(100)); // "" (пустая строка)
```

## 🔄 Основные методы строк

### 🔍 Поиск в строке

```javascript
let text = "JavaScript - лучший язык программирования!";

// indexOf() - позиция первого вхождения
let position = text.indexOf("JavaScript"); // 0
let position2 = text.indexOf("лучший"); // 13
let notFound = text.indexOf("Python"); // -1 (не найден)

// lastIndexOf() - позиция последнего вхождения
let lastPosition = text.lastIndexOf("а"); // 37

// includes() - проверка наличия
let hasJavaScript = text.includes("JavaScript"); // true
let hasPython = text.includes("Python"); // false

// startsWith() и endsWith() - проверка начала и конца
let startsWithJava = text.startsWith("Java"); // true
let endsWithNie = text.endsWith("ния!"); // true

// search() - с регулярными выражениями
let regPosition = text.search(/лучший/); // 13
```

### ✂️ Вырезание подстрок

```javascript
let text = "JavaScript programming language";

// slice(start, end) - вырезать от start до end (не включая)
let piece1 = text.slice(0, 10); // "JavaScript"
let piece2 = text.slice(11); // "programming language"
let end = text.slice(-8); // "language"

// substring(start, end) - как slice, но отрицательные работают иначе
let substring = text.substring(0, 10); // "JavaScript"

// substr(start, length) - устарел, но встречается
let part = text.substr(11, 11); // "programming"
```

### 🔄 Замена в строках

```javascript
let text = "Красный розовый красный цветок";

// replace() - замена только первого вхождения
let changed1 = text.replace("красный", "синий");
// "Красный розовый синий цветок": поиск чувствителен к регистру

// replace() с флагом g - замена всех вхождений
let changed2 = text.replace(/красный/g, "синий");
// "Красный розовый синий цветок"; для обоих регистров нужен флаг gi

// replace() с функцией
let result = text.replace(/красный/g, (match, position) => {
  return `ЗДЕСЬ БЫЛО "${match}" НА ПОЗИЦИИ ${position}`;
});
console.log(result);
```

### 🧹 Изменение регистра

```javascript
let text = "JavaScript Programming Language";

// toUpperCase() - все в верхний регистр
let upper = text.toUpperCase(); // "JAVASCRIPT PROGRAMMING LANGUAGE"

// toLowerCase() - все в нижний регистр
let lower = text.toLowerCase(); // "javascript programming language"

// Первая буква заглавная, остальные строчные
let name = "иван";
let properName = name[0].toUpperCase() + name.slice(1).toLowerCase();
// "Иван"
```

### 🎯 Удаление пробелов

```javascript
let text = "   Привет мир!   ";

// trim() - убрать пробелы по краям
let cleaned = text.trim(); // "Привет мир!"

// trimStart() / trimLeft() - убрать пробелы в начале
let leftSide = text.trimStart(); // "Привет мир!   "

// trimEnd() / trimRight() - убрать пробелы в конце
let rightSide = text.trimEnd(); // "   Привет мир!"
```

## 🔗 Объединение строк

### ➕ Сложение строк

```javascript
let name = "Анна";
let lastName = "Петрова";
let fullName = name + " " + lastName; // "Анна Петрова"

// Для сложения числа и строки
let age = 25;
let text2 = "Мне " + age + " лет"; // "Мне 25 лет"
```

### 🎯 Template literals (современный способ)

```javascript
let name = "Михаил";
let age = 30;
let city = "Москва";

let form = `
Имя: ${name}
Возраст: ${age}
Город: ${city}
Статус: ${age >= 18 ? "совершеннолетний" : "несовершеннолетний"}
`;

console.log(form);
```

### 📋 join() массива в строку

```javascript
let words = ["JavaScript", "это", "супер"];
let sentence = words.join(" "); // "JavaScript это супер"

let fruits = ["яблоко", "банан", "апельсин"];
let list = fruits.join(", "); // "яблоко, банан, апельсин"

let symbols = "JavaScript".split("").join("-"); // "J-a-v-a-S-c-r-i-p-t"
```

## 🔄 Преобразование типов

### ➡️ В строку

```javascript
let number = 42;
let boolean = true;

// String()
let str1 = String(number); // "42"
let str2 = String(boolean); // "true"

// toString()
let str3 = number.toString(); // "42"

// Быстрый способ
let str4 = "" + number; // "42"

// Для объектов
let person = { name: "Вася" };
console.log(person.toString()); // "[object Object]"
```

### ⚠️ Хитрости с преобразованием

```javascript
// Преобразование массива в строку
let array = [1, 2, 3];
console.log(String(array)); // "1,2,3"

// Пустая строка
let empty = "";
console.log(empty.length); // 0

// Пробелы невидимы
let spaces = "   ";
console.log(spaces.length); // 3
```

## 🎯 Практические примеры

### 📧 Учебная проверка строки email

Проверки ниже демонстрируют методы строк и не подтверждают корректность или существование почтового адреса.

```javascript
function validateEmail(email) {
  // Проверка наличия @ и .
  let hasDog = email.includes("@");
  let hasDot = email.includes(".");
  let notStartWithDog = !email.startsWith("@");
  let notEndWithDot = !email.endsWith(".");

  return (
    hasDog &&
    hasDot &&
    notStartWithDog &&
    notEndWithDot
  );
}

console.log(validateEmail("user@example.com")); // true
console.log(validateEmail("@example.com")); // false
console.log(validateEmail("user@example.")); // false
```

### 📝 Форматирование имени

```javascript
function formatName(name) {
  // Убираем пробелы по краям
  name = name.trim();
  if (name === "") return "";

  // Делаем первую букву заглавной
  return name[0].toUpperCase() + name.slice(1).toLowerCase();
}

console.log(formatName("  аННА  ")); // "Анна"
console.log(formatName("пеТР")); // "Петр"
```

### 🔍 Генератор случайной учебной строки

Math.random подходит для этого упражнения, но не для паролей или токенов. Для криптографической случайности предназначен crypto.getRandomValues.

```javascript
function createPassword(length = 8) {
  let symbols =
    "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%";
  let password = "";

  for (let i = 0; i < length; i++) {
    let randomIndex = Math.floor(Math.random() * symbols.length);
    password += symbols[randomIndex];
  }

  return password;
}

console.log(createPassword(12)); // Например, "xK9@mN2!pQ7R"; при каждом запуске результат может отличаться
```

### 🎮 Работа с путями файлов

```javascript
let filePath = "/home/user/documents/файл.txt";

// Получить имя файла
let parts = filePath.split("/");
let fileName = parts[parts.length - 1]; // "файл.txt"

// Получить расширение
let extension = fileName.split(".").pop(); // "txt"

// Получить имя без расширения
let nameWithoutExt = fileName.slice(0, fileName.lastIndexOf(".")); // "файл"

console.log(`Имя: ${nameWithoutExt}, Расширение: ${extension}`);
```

### 📊 Подсчет слов

```javascript
function countWords(text) {
  // Убираем лишние пробелы и разделяем на слова
  const trimmed = text.trim();
  if (trimmed === "") return 0;
  let words = trimmed.split(/\s+/);
  return words.length;
}

let paragraph = "   Это    пример   текста с   разным   количеством   пробелов   ";
console.log(`Слов в тексте: ${countWords(paragraph)}`); // 7
```

### 🔄 Цензура слов

```javascript
function censor(text, forbiddenWords) {
  let result = text;
  for (const word of forbiddenWords) {
    if (word === "") continue;
    const escaped = word.replace(/[.*+?^${}()|[\]\\]/g, "\\$&");
    result = result.replace(new RegExp(escaped, "giu"), (match) => "*".repeat(match.length));
  }
  return result;
}
console.log(censor("Этот ужасный код просто ужасен!", ["ужасный", "ужасен"]));
// "Этот ******* код просто ******!"
console.log(censor("c++ и c--", ["c++"])); // "*** и c--"
// Это буквальная замена фрагментов, а не проверка границ слов.
```

## 🚨 Частые ошибки новичков

### ❌ Строки - неизменяемы!

```javascript
let text = "Привет";
text[0] = "А"; // ❌ Не работает! Строки нельзя изменять по индексу
console.log(text); // "Привет" (не изменилось)

// ✅ Правильно - создаем новую строку
text = "А" + text.slice(1); // "Аривет"
```

### ❌ Путаница с индексами

```javascript
let word = "привет";
console.log(word[word.length]); // ❌ undefined (индексы от 0 до length-1)
console.log(word[word.length - 1]); // ✅ "т"
```

### ❌ Сравнение строк

```javascript
let text1 = "Привет";
let text2 = "привет";

console.log(text1 == text2); // false (разный регистр)
console.log(text1.toLowerCase() == text2.toLowerCase()); // true

// Лексикографическое сравнение
console.log("яблоко" > "апельсин"); // true (потому что 'я' > 'а')
```

### ❌ Unicode символы

```javascript
let emoji = "👨‍👩‍👧‍👦"; // Семья
console.log(emoji.length); // 11 (сложный эмодзи состоит из нескольких символов)

// Spread перебирает кодовые точки, а не видимые символы.
console.log([...emoji].length); // 7
const segmenter = new Intl.Segmenter("ru", { granularity: "grapheme" });
console.log([...segmenter.segment(emoji)].length); // 1 графема
```

## 📚 Шпаргалка быстрых операций

| Задача              | Метод                   | Пример                   |
| ------------------- | ----------------------- | ------------------------ |
| Узнать длину        | `str.length`            | `text.length`            |
| Доступ к символу    | `str[index]`            | `text[0]`                |
| Найти позицию       | `str.indexOf()`         | `text.indexOf("a")`      |
| Проверить наличие   | `str.includes()`        | `text.includes("a")`     |
| Вырезать часть      | `str.slice(start, end)` | `text.slice(0, 5)`       |
| Заменить            | `str.replace(old, new)` | `text.replace("a", "b")` |
| В верхний регистр   | `str.toUpperCase()`     | `text.toUpperCase()`     |
| В нижний регистр    | `str.toLowerCase()`     | `text.toLowerCase()`     |
| Убрать пробелы      | `str.trim()`            | `text.trim()`            |
| Разделить на массив | `str.split()`           | `text.split(" ")`        |

## 🎮 Практика в консоли

Открой F12 и попробуй:

```javascript
// Создай предложение
let sentence = "JavaScript - мощный язык программирования";

// Узнай длину
console.log("Длина:", sentence.length);

// Найди позицию слова
console.log("Позиция 'мощный':", sentence.indexOf("мощный"));

// Сделай все заглавными
console.log("Заглавными:", sentence.toUpperCase());

// Раздели на слова
let words = sentence.split(" ");
console.log("Слова:", words);

// Создай новую строку
let greeting = `Мой любимый язык - ${words[0]}!`;
console.log(greeting);

// Посчитай гласные
let vowels = "аеёиоуыэюяАЕЁИОУЫЭЮЯ";
let vowelsCount = [...sentence].filter((letter) =>
  vowels.includes(letter),
).length;
console.log(`Гласных в предложении: ${vowelsCount}`);
```


## 📝 Задания для закрепления

### Задание 1: Заглавные буквы
Напиши функцию `capitalize(str)`, которая делает первую букву каждого слова заглавной.
```javascript
capitalize("привет мир");          // "Привет Мир"
capitalize("javascript для всех"); // "Javascript Для Всех"
```

### Задание 2: Палиндром
Напиши функцию `isPalindrome(str)`, которая проверяет, является ли строка палиндромом. Игнорируй пробелы и регистр.
```javascript
isPalindrome("шалаш");       // true
isPalindrome("Анна");        // true
isPalindrome("привет");      // false
isPalindrome("А роза упала на лапу Азора"); // true
```

### Задание 3: Обрезка строки
Напиши функцию `truncate(str, maxLength)`, которая обрезает строку до `maxLength` символов и добавляет `"..."`, если строка длиннее.
```javascript
truncate("Привет мир!", 7);  // "Привет ..."
truncate("Привет", 10);     // "Привет"
```

### Задание 4: Подсчёт гласных
Напиши функцию `countVowels(str)`, которая считает количество гласных букв (а, е, ё, и, о, у, ы, э, ю, я) в строке. Регистр не важен.

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** Строки - это как цепочки букв, которые можно соединять, резать и искать, но нельзя изменять по частям! 🔗

Используй методы строк, и работа с текстом станет легкой и приятной! 📝

## Документация

- [String — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)
- [Графемы и Intl.Segmenter — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Segmenter)


---

[⬅️ Предыдущая тема: Циклы](loops-js.md) | [📚 Оглавление](README.md) | [Следующая тема: Массивы ➡️](arrays-js.md)
