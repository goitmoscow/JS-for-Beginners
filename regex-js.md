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
// ["999", index: 14, input: "Телефон: +7(999)123-45-67", groups: undefined]

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
console.log(result2); // "Я люблю 🍎(16) и 🍎(29)"
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
console.log(/Привет.../.test(text)); // false (только 3 символа после Привет)

// ^ - начало строки
console.log(/^Привет/.test(текст)); // true

// $ - конец строки
console.log(/мир!$/.test(текст)); // true

// | - или (альтернатива)
console.log(/Привет|Пока/.test(текст)); // true
```

### 🎯 Квантификаторы

```javascript
const text = "aa aaa aaaaa";

// * - 0 или более раз
console.log(/a*/.test("")); // true (0 раз)
console.log(/a*/.exec("aaa")); // "aaa"

// + - 1 или более раз
console.log(/a+/.exec("")); // null
console.log(/a+/.exec("aaa")); // "aaa"

// ? - 0 или 1 раз
console.log(/colou?r/.test("color")); // true
console.log(/colou?r/.test("colour")); // true

// {n} - ровно n раз
console.log(/a{3}/.test("aaa")); // true
console.log(/a{3}/.test("aa")); // false

// {n,m} - от n до m раз
console.log(/a{2,4}/.test("aa")); // true
console.log(/a{2,4}/.test("aaaa")); // true
console.log(/a{2,4}/.test("aaaaa")); // false

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
console.log(/[^abc]/.test(текст)); // true

// [a-z] - любая маленькая буква
console.log(/[a-z]/.test(текст)); // true

// [A-Z] - любая большая буква
console.log(/[A-Z]/.test(текст)); // false

// [0-9] - любая цифра
console.log(/[0-9]/.test(текст)); // true

// [a-zA-Z0-9] - буквы и цифры
console.log(/[a-zA-Z0-9]/.test(текст)); // true
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

// \s - пробельный символ [\t\n\r\f\v]
console.log(/\s/.test("hello world")); // true

// \S - не пробельный символ
console.log(/\S/.test("helloworld")); // true
```

## 🎯 Группы и скобки

### 🎯 Скобочные группы

```javascript
const text = "Иван Иванов, email: ivan@example.com";

// Группа (...)
const pattern = /(\w+)\s+(\w+)/;
const result = pattern.exec(text);
console.log(result);
// ["Иван Иванов", "Иван", "Иванов", index: 0, input: "...", groups: undefined]

console.log(result[0]); // "Иван Иванов" (все совпадение)
console.log(result[1]); // "Иван" (первая группа)
console.log(result[2]); // "Иванов" (вторая группа)

// Именованные группы
const pattern2 = /(?<name>\w+)\s+(?<surname>\w+)/;
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
const nonCapturing = /(\d{4})(?:-(\d{2})(?:-(\d{2}))?)/;
const result2 = nonCapturing.exec(text);
console.log(result2.length); // 3 (только нужные группы)
```

### 🎯 Опережающие проверки (?=)

```javascript
const text = "windows2000 windows10 windows11";

// Найти "windows" перед цифрами
const pattern = /windows(?=\d+)/;
console.log(text.match(pattern)); // ["windows", "windows", "windows"]

// Найти "windows" не перед "XP"
const pattern2 = /windows(?!XP)/;
console.log(pattern2.test("windowsXP")); // false
console.log(pattern2.test("windows10")); // true
```

## 🎯 Практические примеры

### 📧 Валидация email

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
  // Формат: +7(999)123-45-67 или 8(999)123-45-67
  const pattern =
    /^(\+7|8)?\(?(\d{3})\)?[\s-]?(\d{3})[\s-]?(\d{2})[\s-]?(\d{2})$/;
  const result = pattern.exec(phone.replace(/[\s()-]/g, ""));

  if (result) {
    return {
      code: result[1],
      areaCode: result[2],
      firstTriple: result[3],
      secondPair: result[4],
      thirdPair: result[5],
      formatted: `+7(${result[2]})${result[3]}-${result[4]}-${result[5]}`,
    };
  }

  return null;
}

console.log(validatePhone("+7(999)123-45-67"));
// { code: "+7", areaCode: "999", firstTriple: "123", secondPair: "45", thirdPair: "67", formatted: "+7(999)123-45-67" }
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
  const pattern = /(?:\$|€|₽|₴)?(\d+(?:\.\d{2})?)\s?(?:USD|EUR|RUB|USD)?/gi;
  const matches = [];
  let result;

  while ((result = pattern.exec(text)) !== null) {
    matches.push({
      amount: parseFloat(result[1]),
      currency: result[0].includes("$")
        ? "USD"
        : result[0].includes("€")
          ? "EUR"
          : result[0].includes("₽")
            ? "RUB"
            : "USD",
      full: result[0],
    });
  }

  return matches;
}

const text = "Цены: $100.50, €200, ₽1500.75, 300 USD";
const prices = extractPrices(text);
console.log(prices);
// [
//   { amount: 100.5, currency: 'USD', full: '$100.50' },
//   { amount: 200, currency: 'EUR', full: '€200' },
//   { amount: 1500.75, currency: 'RUB', full: '₽1500.75' },
//   { amount: 300, currency: 'USD', full: '300 USD' }
// ]
```

### 🏷️ Извлечение хэштегов

```javascript
function extractHashtags(text) {
  const pattern = /#(\w+)/g;
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
function parseCSV(csv_строка) {
  const lines = csv_строка.split("\n");
  const result = [];

  for (const line of lines) {
    if (!line.trim()) continue;

    const pattern = /("([^"]*)"|([^,]*))/g;
    const fields = [];
    let match;

    while ((match = pattern.exec(line)) !== null) {
      const value = match[1] || match[2];
      fields.push(value.trim());
    }

    if (fields.length > 0) {
      result.push(fields);
    }
  }

  return result;
}

const csv = `Имя,Возраст,Город
"Иван Петров",25,"Москва"
Анна,30,"Санкт-Петербург"
"Борис \"Боб\"",35,Новосибирск`;

const data = parseCSV(csv);
console.log(data);
// [
//   ["Имя", "Возраст", "Город"],
//   ["Иван Петров", "25", "Москва"],
//   ["Анна", "30", "Санкт-Петербург"],
//   ['Борис "Боб"', "35", "Новосибирск"]
// ]
```

## 🎯 Комплексные примеры

### 📝 Markdown в HTML

```javascript
function markdownToHTML(markdown) {
  // Заголовки
  let html = markdown.replace(/^### (.*$)/gim, "<h3>$1</h3>");
  html = html.replace(/^## (.*$)/gim, "<h2>$1</h2>");
  html = html.replace(/^# (.*$)/gim, "<h1>$1</h1>");

  // Жирный текст
  html = html.replace(/\*\*(.*?)\*\*/g, "<strong>$1</strong>");

  // Курсив
  html = html.replace(/\*(.*?)\*/g, "<em>$1</em>");

  // Ссылки
  html = html.replace(/\[([^\]]+)\]\(([^)]+)\)/g, '<a href="$2">$1</a>');

  // Код (внутри `)
  html = html.replace(/`([^`]+)`/g, "<code>$1</code>");

  // Параграфы (любой текст не в тегах)
  html = html.replace(/^(?!<[h|a|c|s|p]).*$/gm, "<p>$&</p>");

  return html;
}

const text = `# Привет мир

Это **тестовый** текст со *курсивом* и \`кодом\`.

[Ссылка на Google](https://google.com)

## Подзаголовок

### Еще один подзаголовок`;

console.log(markdownToHTML(text));
```

### 🔍 Поиск и замена с контекстом

```javascript
function replaceWordContext(text, word, replacement) {
  const pattern = new RegExp(`\\b(\w*${word}\w*)\\b`, "gi");

  return text.replace(pattern, (match) => {
    return match.toLowerCase() === word.toLowerCase()
      ? replacement
      : match;
  });
}

const text = "JavaScript - это язык программирования. Я люблю JavaScript!";
const result = replaceWordContext(text, "javascript", "JS");
console.log(result);
// "JS - это язык программирования. Я люблю JS!"
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
console.log(/C:\\Windows/.test("C:\Windows")); // true

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
// ❌ ПЛОХО - флаги переданы как один параметр
const pattern1 = new RegExp("test", "gi"); // Правильно

// ❌ ПЛОХО - забыт экранирование в строке
const pattern2 = new RegExp("\d+"); // Ищет "d+", а не цифры

// ✅ ХОРОШО
const pattern3 = new RegExp("\\d+"); // Ищет цифры
```

## 📚 Шпаргалка быстрых шаблонов

| Задача           | Шаблон                                                                     | Пример                     |
| ---------------- | -------------------------------------------------------------------------- | -------------------------- | -------------------------------- | ----------- | ------------------- | ------------- |
| Email            | `/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/`                       | `test@example.com`         |
| Телефон          | `/^\+?\d{1,3}[-\s]?\(?\d{1,4}\)?[-\s]?\d{1,4}[-\s]?\d{1,4}[-\s]?\d{1,9}$/` | `+7(999)123-45-67`         |
| URL              | `/https?:\/\/(?:[-\w.])+(?:[:\d]+)?(?:\/(?:[^\s()]*)?)?/`                  | `https://example.com/path` |
| IPv4             | `/^(?:(?:25[0-5]                                                           | 2[0-4][0-9]                | [01]?[0-9][0-9])\.){3}(?:25[0-5] | 2[0-4][0-9] | [01]?[0-9][0-9])$/` | `192.168.1.1` |
| Дата             | `/^\d{4}-\d{2}-\d{2}$/`                                                    | `2023-10-25`               |
| Только буквы     | `/^[a-zA-Zа-яА-Я]+$/`                                                      | `Привет`                   |
| Только цифры     | `/^\d+$/`                                                                  | `12345`                    |
| Пароль (сильный) | `/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d]{8,}$/`                         | `Password123`              |

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
const words = text2.match(/\b\w+\b/g);
console.log("Слова:", words);

// 4. Поиск хэштегов
const post = "Сегодня #погода отличная! #прогулка #парк";
const hashtags = post.match(/#\w+/g);
console.log("Хэштеги:", hashtags);

// 5. Замена слов
const text3 = "cat dog cat mouse";
const replaced = text3.replace(/cat/g, "кошка");
console.log("Замененный текст:", replaced);

// 6. Проверка на сильный пароль
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
const domains = urls.match(/https?:\/\/([^\/]+)/g);
console.log("Домены:", domains);
```

---

**Запомни главное:** Регулярные выражения - это мощный инструмент для поиска и обработки текста по шаблонам! Используй их для валидации, парсинга и сложных замен. 🔍

Регулярные выражения - это как умный поиск Ctrl+F с возможностями супергероя! 🦸‍♂️📝
