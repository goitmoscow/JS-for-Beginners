# Регулярные выражения 🔍

## 🎦 Что такое регулярные выражения?

Представь регулярные выражения как **умный поиск по тексту**:

🔍 **Простой поиск** = найти конкретное слово  
🧠 **Регулярное выражение** = найти слова по шаблону  
📝 **Шаблон** = правила поиска (буквы, цифры, паттерны)

```javascript
const text = "Мой телефон: +7(999)123-45-67";
const pattern = /\+?\d?\(?\d{3}\)?[\s-]?\d{3}[\s-]?\d{2}[\s-]?\d{2}/;
const found = pattern.exec(text);
console.log(found[0]); // "+7(999)123-45-67"
```

## 🎯 Создание регулярных выражений

### 🎯 Способ 1: литералы

```javascript
const pattern1 = /hello/; // Простой поиск
const pattern2 = /hello/i; // i - регистронезависимый
const pattern3 = /hello/g; // g - глобальный поиск (все вхождения)
const pattern4 = /hello/gi; // gi - глобальный и регистронезависимый
```

### 🎯 Способ 2: конструктор

```javascript
const pattern1 = new RegExp("hello"); // Эквивалент /hello/
const pattern2 = new RegExp("hello", "i"); // /hello/i
const pattern3 = new RegExp("hello", "gi"); // /hello/gi

// Динамическое создание
const word = "java";
const pattern = new RegExp(word + "script", "i"); // /javascript/i
```

## 🔍 Основные методы

### 🎯 test() - проверка наличия

```javascript
const text = "Привет мир!";
const pattern = /привет/i;

console.log(pattern.test(text)); // true

const pattern2 = /пока/;
console.log(pattern2.test(text)); // false
```

### 🎯 exec() - поиск совпадений

```javascript
const text = "Телефон: +7(999)123-45-67";
const pattern = /\d{3}/;

let result = pattern.exec(text);
console.log(result);
// ["999", index: 12, input: "Телефон: +7(999)123-45-67", groups: undefined]

// С глобальным флагом
const global = /\d{3}/g;
while ((result = global.exec(text)) !== null) {
  console.log(`Найдено: ${result[0]} на позиции ${result.index}`);
}
```

### 🎯 match() - поиск в строке

```javascript
const text = "cat dog cat mouse";

// Без флага g
console.log(text.match(/cat/));
// ["cat", index: 0, input: "cat dog cat mouse", groups: undefined]

// С флагом g
console.log(text.match(/cat/g));
// ["cat", "cat"]
```

### 🎯 replace() - замена

```javascript
const text = "Я люблю яблоки и яблоки";
const result1 = text.replace(/яблоки/g, "апельсины");
console.log(result1); // "Я люблю апельсины и апельсины"

// С функцией
const result2 = text.replace(/яблоки/g, (match, index) => {
  return `🍎(${index})`;
});
console.log(result2); // "Я люблю 🍎(8) и 🍎(17)"
```

### 🎯 split() - разделение

```javascript
const text = "apple,banana;cherry|date";
const delimiters = /[;,|]/;
const fruits = text.split(delimiters);
console.log(fruits); // ["apple", "banana", "cherry", "date"]
```

## 🎨 Специальные символы

### 🎯 Основные метасимволы

```javascript
const text = "Привет123 мир!";

// . - любой символ кроме перевода строки
console.log(/Привет.../.test(text)); // true: найдена подстрока "Привет123", полный текст не обязан совпасть

// ^ - начало строки
console.log(/^Привет/.test(text)); // true

// $ - конец строки
console.log(/мир!$/.test(text)); // true

// | - или (альтернатива)
console.log(/Привет|Пока/.test(text)); // true
```

### 🎯 Квантификаторы

```javascript
const text = "aa aaa aaaaa";

// * - 0 или более раз
console.log(/a*/.test("")); // true (0 раз)
console.log(/a*/.exec("aaa")[0]); // "aaa": берём полное совпадение из массива

// + - 1 или более раз
console.log(/a+/.exec("")); // null
console.log(/a+/.exec("aaa")[0]); // "aaa"

// ? - 0 или 1 раз
console.log(/colou?r/.test("color")); // true
console.log(/colou?r/.test("colour")); // true

// {n} - ровно n раз
console.log(/a{3}/.test("aaa")); // true
console.log(/a{3}/.test("aa")); // false

// {n,m} - от n до m раз
console.log(/a{2,4}/.test("aa")); // true
console.log(/a{2,4}/.test("aaaa")); // true
console.log(/a{2,4}/.test("aaaaa")); // true: подходит подстрока
console.log(/^a{2,4}$/.test("aaaaa")); // false: якоря требуют всю строку

// {n,} - n или более раз
console.log(/a{2,}/.test("aa")); // true
console.log(/a{2,}/.test("aaaaa")); // true
```

### 🎯 Жадные и ленивые квантификаторы

```javascript
const text = "<div>Содержимое</div><div>Еще</div>";

// Жадный (по умолчанию) - максимальное совпадение
const greedy = /<div>.*<\/div>/;
console.log(greedy.exec(text)[0]); // "<div>Содержимое</div><div>Еще</div>"

// Ленивый - минимальное совпадение
const lazy = /<div>.*?<\/div>/;
console.log(lazy.exec(text)[0]); // "<div>Содержимое</div>"
```

## 📋 Наборы символов

### 🎯 Основные наборы

```javascript
const text = "abc123!@#";

// [abc] - любой из символов a, b, c
console.log(/[abc]/.test(text)); // true

// [^abc] - любой символ кроме a, b, c
console.log(/[^abc]/.test(text)); // true

// [a-z] - любая маленькая буква
console.log(/[a-z]/.test(text)); // true

// [A-Z] - любая большая буква
console.log(/[A-Z]/.test(text)); // false

// [0-9] - любая цифра
console.log(/[0-9]/.test(text)); // true

// [a-zA-Z0-9] - буквы и цифры
console.log(/[a-zA-Z0-9]/.test(text)); // true
```

### 🎯 Классы символов (сокращения)

```javascript
// \d - цифра [0-9]
console.log(/\d/.test("abc123")); // true

// \D - не цифра [^0-9]
console.log(/\D/.test("abc123")); // true

// \w - слово [a-zA-Z0-9_]
console.log(/\w/.test("hello_world")); // true

// \W - не слово [^a-zA-Z0-9_]
console.log(/\W/.test("hello@world")); // true

// \s — пробельный символ: обычный пробел, \t, \n и другие Unicode-пробелы
console.log(/\s/.test("hello world")); // true

// \S - не пробельный символ
console.log(/\S/.test("helloworld")); // true
```

## 🎯 Группы и скобки

\w включает латинские буквы, цифры и _, но не русские буквы. Для букв Unicode используйте \p{L} с флагом u; \p{M} позволяет учитывать комбинируемые знаки. test без ^ и $ ищет совпадающую часть, а не проверяет весь ввод.

### 🎯 Скобочные группы

```javascript
const text = "Иван Иванов, email: ivan@example.com";

// Группа (...)
const pattern = /([\p{L}\p{M}]+)\s+([\p{L}\p{M}]+)/u;
const result = pattern.exec(text);
console.log(result);
// ["Иван Иванов", "Иван", "Иванов", index: 0, input: "...", groups: undefined]

console.log(result[0]); // "Иван Иванов" (все совпадение)
console.log(result[1]); // "Иван" (первая группа)
console.log(result[2]); // "Иванов" (вторая группа)

// Именованные группы
const pattern2 = /(?<name>[\p{L}\p{M}]+)\s+(?<surname>[\p{L}\p{M}]+)/u;
const result2 = pattern2.exec(text);
console.log(result2.groups); // {name: "Иван", surname: "Иванов"}
```

### 🎯 Незахватывающие группы (?:)

```javascript
const text = "2023-10-25";

// Захватывающая группа
const capturing = /(\d{4})-(\d{2})-(\d{2})/;
const result1 = capturing.exec(text);
console.log(result1.length); // 4 (включая полное совпадение)

// Незахватывающая группа
const nonCapturing = /(\d{4})-(\d{2})(?:-\d{2})?/;
const result2 = nonCapturing.exec(text);
console.log(result2.length); // 3 (только нужные группы)
```

### 🎯 Опережающие проверки (?=)

```javascript
const text = "windows2000 windows10 windows11";

// Найти "windows" перед цифрами
const pattern = /windows(?=\d+)/g;
console.log(text.match(pattern)); // ["windows", "windows", "windows"]

// Найти "windows" не перед "XP"
const pattern2 = /windows(?!XP)/;
console.log(pattern2.test("windowsXP")); // false
console.log(pattern2.test("windows10")); // true
```

## 🎯 Практические примеры

### 📧 Учебная проверка email

Регулярное выражение иллюстрирует формат, но не доказывает существование адреса и не покрывает все допустимые адреса. Аналогично, шаблон даты ниже проверяет запись, а не календарную корректность.

```javascript
function validateEmail(email) {
  const pattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
  return pattern.test(email);
}

console.log(validateEmail("user@example.com")); // true
console.log(validateEmail("user.name@domain.co.uk")); // true
console.log(validateEmail("invalid.email")); // false
console.log(validateEmail("@domain.com")); // false
```

### 📞 Валидация телефона

```javascript
function validatePhone(phone) {
  const valid = /^(?:\+7|8)(?:\d{10}|\(\d{3}\)\d{3}-\d{2}-\d{2})$/;
  if (!valid.test(phone)) return null;
  const digits = phone.replace(/\D/g, "");
  const code = phone.startsWith("+7") ? "+7" : "8";
  const areaCode = digits.slice(1, 4);
  const firstTriple = digits.slice(4, 7);
  const secondPair = digits.slice(7, 9);
  const thirdPair = digits.slice(9, 11);
  return { code, areaCode, firstTriple, secondPair, thirdPair,
    formatted: `+7(${areaCode})${firstTriple}-${secondPair}-${thirdPair}` };
}
console.log(validatePhone("+7(999)123-45-67").formatted); // "+7(999)123-45-67"
console.log(validatePhone("+7(999123-45-67")); // null: скобки должны быть парными
```

### 🔍 Поиск URL в тексте

```javascript
function findUrls(text) {
  const pattern =
    /https?:\/\/(?:[-\w.])+(?:[:]\d+)?(?:\/(?:[^\s()]*\([^)]*\)[^\s()]*|[^\s()]*)?)?/g;
  return text.match(pattern) || [];
}

const text = `
Посетите https://example.com или http://test.org/path/to/page
Также есть https://subdomain.domain.com:8080/api/data
`;

const urls = findUrls(text);
console.log(urls);
// ["https://example.com", "http://test.org/path/to/page", "https://subdomain.domain.com:8080/api/data"]
```

### 💰 Извлечение цен

```javascript
function extractPrices(text) {
  const pattern = /([$€₽])\s*(\d+(?:\.\d{1,2})?)|(\d+(?:\.\d{1,2})?)\s*(USD|EUR|RUB)\b/gi;
  const symbols = { "$": "USD", "€": "EUR", "₽": "RUB" };
  return [...text.matchAll(pattern)].map((match) => ({
    amount: Number(match[2] ?? match[3]),
    currency: match[1] ? symbols[match[1]] : match[4].toUpperCase(),
    full: match[0],
  }));
}
console.log(extractPrices("Цены: $100.50, €200, ₽1500.75, 300 USD"));
// Валюта берётся из символа или буквенного кода, а не назначается по умолчанию.
```

### 🏷️ Извлечение хэштегов

```javascript
function extractHashtags(text) {
  const pattern = /#([\p{L}\p{M}\p{N}_]+)/gu;
  const matches = [];
  let result;

  while ((result = pattern.exec(text)) !== null) {
    matches.push(result[1]); // только текст без #
  }

  return matches;
}

const post = "Сегодня #погода отличная! Прогулка #парк #солнце";
const hashtags = extractHashtags(post);
console.log(hashtags); // ["погода", "парк", "солнце"]
```

### 🔧 Удаление лишних пробелов

```javascript
function removeSpaces(text) {
  // Удаляем пробелы в начале и конце
  // Заменяем множественные пробелы на один
  return text.replace(/^\s+|\s+$/g, "").replace(/\s+/g, " ");
}

console.log(removeSpaces("   Привет    мир!   ")); // "Привет мир!"
```

### 📊 Парсинг CSV

```javascript
// Учебный вариант: запятые, пустые поля, двойные кавычки и CRLF.
// Переносы строки внутри quoted-поля здесь не поддерживаются.
function parseCSV(csv) {
  if (csv === "") return [];
  return csv.split(/\r?\n/).filter((line) => line !== "").map((line) => {
    const fields = [];
    let field = "";
    let quoted = false;
    for (let i = 0; i < line.length; i++) {
      const char = line[i];
      if (char === '"') {
        if (quoted && line[i + 1] === '"') { field += '"'; i++; }
        else quoted = !quoted;
      } else if (char === "," && !quoted) {
        fields.push(field);
        field = "";
      } else {
        field += char;
      }
    }
    if (quoted) throw new SyntaxError("Незакрытая кавычка CSV");
    fields.push(field);
    return fields;
  });
}
const csv = `Имя,Возраст,Город
"Иван Петров",25,"Москва"
Анна,30,"Санкт-Петербург"
"Борис ""Боб""",35,Новосибирск`;
console.log(parseCSV(csv));
// Последняя строка: ['Борис "Боб"', "35", "Новосибирск"]
// Цикл всегда продвигает индекс; regex с пустыми совпадениями мог бы зациклиться.
```

## 🎯 Комплексные примеры

### 📝 Markdown в HTML

```javascript
// Небольшой учебный поднабор: заголовки, выделение и HTTP(S)-ссылки.
// Это не полноценный Markdown-парсер; порядок замен ограничивает поддерживаемую разметку.
function markdownToHTML(markdown) {
  const escape = (text) => text.replace(/&/g, "&amp;").replace(/</g, "&lt;")
    .replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/\x27/g, "&#39;");
  let html = escape(markdown);
  html = html.replace(/^### (.+)$/gm, "<h3>$1</h3>");
  html = html.replace(/^## (.+)$/gm, "<h2>$1</h2>");
  html = html.replace(/^# (.+)$/gm, "<h1>$1</h1>");
  html = html.replace(/\*\*(.+?)\*\*/g, "<strong>$1</strong>");
  html = html.replace(/\*([^*]+)\*/g, "<em>$1</em>");
  html = html.replace(/\[([^\]]+)\]\((https?:\/\/[^)\s]+)\)/g, '<a href="$2">$1</a>');
  return html.split("\n").filter(Boolean).map((line) =>
    /^<h[1-3]>/.test(line) ? line : `<p>${line}</p>`
  ).join("\n");
}
console.log(markdownToHTML("# Пример\n\n**Выделение** и [ссылка](https://example.com)"));
console.log(markdownToHTML("<img src=x>")); // Текст экранирован, HTML-тег не создан
```

### 🔍 Поиск и замена с контекстом

```javascript
function replaceWordContext(text, word, replacement) {
  if (word === "") return text;
  const escaped = word.replace(/[.*+?^${}()|[\]\\]/g, "\\$&");
  // Unicode-границы: буквы, цифры и _ считаем частью слова.
  const pattern = new RegExp(`(^|[^\\p{L}\\p{M}\\p{N}_])${escaped}(?=$|[^\\p{L}\\p{M}\\p{N}_])`, "giu");
  return text.replace(pattern, (_, prefix) => prefix + replacement);
}
console.log(replaceWordContext("JavaScript и JavaScript!", "javascript", "JS")); // "JS и JS!"
console.log(replaceWordContext("кот и котик", "кот", "пёс")); // "пёс и котик"
```

## 🚨 Частые ошибки новичков

### ❌ Забытый флаг глобального поиска

```javascript
const text = "cat dog cat";

// ❌ ПЛОХО - найдет только первое совпадение
console.log(text.replace(/cat/, "dog")); // "dog dog cat"

// ✅ ХОРОШО - заменит все совпадения
console.log(text.replace(/cat/g, "dog")); // "dog dog dog"
```

### ❌ Неправильное экранирование

```javascript
// ❌ ПЛОХО - не экранирован обратный слэш
console.log(/C:\Windows/.test("C:\Windows")); // false

// ✅ ХОРОШО - экранируем специальный символ
console.log(/C:\\Windows/.test("C:\\Windows")); // true

// Или используем конструктор для динамических путей
const path = "C:\\Windows";
const pattern = new RegExp(path.replace(/\\/g, "\\\\"));
```

### ❌ Слишком жадные совпадения

```javascript
const text = "<div>Контент</div><div>Еще</div>";

// ❌ ПЛОХО - захватит все от первого <div> до последнего </div>
console.log(text.match(/<div>.*<\/div>/)[0]); // "<div>Контент</div><div>Еще</div>"

// ✅ ХОРОШО - ленивый поиск
console.log(text.match(/<div>.*?<\/div>/)[0]); // "<div>Контент</div>"
```

### ❌ Неправильное использование флагов в конструкторе

```javascript
// ✅ Флаги передаются отдельным вторым аргументом
const pattern1 = new RegExp("test", "gi");

// ❌ ПЛОХО - забыт экранирование в строке
const pattern2 = new RegExp("\d+"); // Ищет "d+", а не цифры

// ✅ ХОРОШО
const pattern3 = new RegExp("\\d+"); // Ищет цифры
```

## 📚 Шпаргалка быстрых шаблонов

| Задача           | Шаблон                                                                     | Пример                     |
| ---------------- | -------------------------------------------------------------------------- | -------------------------- |
| Email            | `/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/`                       | `test@example.com`         |
| Телефон          | `/^\+?\d{1,3}[-\s]?\(?\d{1,4}\)?[-\s]?\d{1,4}[-\s]?\d{1,4}[-\s]?\d{1,9}$/` | `+7(999)123-45-67`         |
| URL              | `/https?:\/\/(?:[-\w.])+(?:[:\d]+)?(?:\/(?:[^\s()]*)?)?/`                  | `https://example.com/path` |
| IPv4 | `/^(?:(?:25[0-5]\|2[0-4]\d\|1\d{2}\|[1-9]?\d)\.){3}(?:25[0-5]\|2[0-4]\d\|1\d{2}\|[1-9]?\d)$/` | `192.168.1.1` |
| Дата             | `/^\d{4}-\d{2}-\d{2}$/`                                                    | `2023-10-25`               |
| Только буквы     | `/^[a-zA-Zа-яА-Я]+$/`                                                      | `Привет`                   |
| Только цифры     | `/^\d+$/`                                                                  | `12345`                    |
| Учебный пароль | `/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d]{8,}$/`                         | `Password123`              |

## 🎮 Практика в консоли

Открой F12 и попробуй:

```javascript
// 1. Поиск цифр
const text1 = "abc123def456";
const numbers = text1.match(/\d+/g);
console.log("Цифры:", numbers);

// 2. Валидация email
function validateEmail(email) {
  const pattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
  return pattern.test(email);
}
console.log("Email валиден:", validateEmail("test@example.com"));
console.log("Email невалиден:", validateEmail("invalid-email"));

// 3. Извлечение слов
const text2 = "Привет мир! Как дела, мир?";
const words = text2.match(/[\p{L}\p{M}]+/gu);
console.log("Слова:", words);

// 4. Поиск хэштегов
const post = "Сегодня #погода отличная! #прогулка #парк";
const hashtags = post.match(/#[\p{L}\p{M}\p{N}_]+/gu);
console.log("Хэштеги:", hashtags);

// 5. Замена слов
const text3 = "cat dog cat mouse";
const replaced = text3.replace(/cat/g, "кошка");
console.log("Замененный текст:", replaced);

// 6. Проверка на учебные требования к паролю
function strongPassword(password) {
  const pattern = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d]{8,}$/;
  return pattern.test(password);
}
console.log("Сильный пароль:", strongPassword("Password123"));
console.log("Слабый пароль:", strongPassword("weak"));

// 7. Извлечение чисел с текстом
const text4 = "Цены: 100$, 250€, 500₽";
const prices = text4.match(/\d+(?=\$|€|₽)/g);
console.log("Цены:", prices);

// 8. Удаление HTML тегов
const html = "<p>Привет <b>мир</b>!</p>";
const cleanText = html.replace(/<[^>]*>/g, "");
console.log("Чистый текст:", cleanText);

// 9. Поиск дат в формате YYYY-MM-DD
const text5 = "События: 2023-10-25 и 2024-01-15";
const dates = text5.match(/\d{4}-\d{2}-\d{2}/g);
console.log("Даты:", dates);

// 10. Извлечение доменов из URL
const urls = "https://example.com http://test.org/path";
const domains = [...urls.matchAll(/https?:\/\/([^/\s]+)/g)].map((match) => match[1]);
console.log("Домены:", domains); // ["example.com", "test.org"]
```

## 📝 Задания для закрепления

### Задание 1: Валидация телефона
Напиши регулярное выражение, которое проверяет российский номер телефона. Допустимые форматы: `+79991234567`, `89991234567`, `+7(999)123-45-67`, `8(999)123-45-67`.

### Задание 2: Извлечение email
Напиши функцию `extractEmails(text)`, которая находит все email-адреса в тексте и возвращает их массивом.
```javascript
extractEmails("Пишите на test@mail.ru или admin@site.com");
// ["test@mail.ru", "admin@site.com"]
```

### Задание 3: Маскировка карты
Напиши функцию `maskCard(number)`, которая маскирует номер банковской карты: видны только последние 4 цифры, остальные заменяются звёздочками.
```javascript
maskCard("1234567890123456"); // "****-****-****-3456"
```

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** Регулярные выражения - это мощный инструмент для поиска и обработки текста по шаблонам! Используй их для валидации, парсинга и сложных замен. 🔍

Регулярные выражения - это как умный поиск Ctrl+F с возможностями супергероя! 🦸‍♂️📝

## Документация

- [Классы символов — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Regular_expressions/Character_class_escape)


---

[⬅️ Предыдущая тема: Обработка ошибок](error-handling.md) | [📚 Оглавление](README.md) | [Следующая тема: JSON и API ➡️](json-api.md)
