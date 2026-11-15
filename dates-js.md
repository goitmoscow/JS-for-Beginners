# Работа с датами и временем 📅

## 🎦 Что такое Date в JavaScript?

Представь Date как **умные часы с календарем**:

🕐 **Время** = часы, минуты, секунды  
📅 **Дата** = день, месяц, год  
🌍 **Часовой пояс** = время в разных частях мира

```javascript
const now = new Date();
console.log(now); // Текущая дата и время
```

## 🕐 Создание дат

### 🎯 Текущая дата

```javascript
const now = new Date();
console.log(now); // Wed Oct 25 2023 15:30:45 GMT+0300
```

### 🎯 Дата из строки

```javascript
const dateFromString = new Date("2023-10-25T15:30:00");
const readableDate = new Date("October 25, 2023 15:30:00");
const russianDate = new Date("25.10.2023 15:30"); // Может не работать везде!

console.log(dateFromString);
console.log(readableDate);
```

### 🎯 Дата из чисел

```javascript
// new Date(год, месяц_0_11, день, часы, минуты, секунды, миллисекунды)
const dateFromNumbers = new Date(2023, 9, 25, 15, 30, 0, 0); // Месяцы с 0!
const dateOnly = new Date(2023, 9, 25); // 25 октября 2023, 00:00:00

console.log(dateFromNumbers);
console.log(dateOnly);
```

### 🎯 Дата из миллисекунд

```javascript
// Unix timestamp - миллисекунды с 1 января 1970 года
const milliseconds = Date.now(); // Текущее время в миллисекундах
const fromMilliseconds = new Date(milliseconds);

console.log("Текущие миллисекунды:", milliseconds);
console.log("Из миллисекунд:", fromMilliseconds);

// Большое число - далекое будущее
const future = new Date(9999999999999);
console.log("Будущее:", future);
```

## 📊 Получение компонентов даты

### 🎯 Основные getters

```javascript
const date = new Date(2023, 9, 25, 15, 30, 45, 123);

// Год (4 цифры)
console.log("Год:", date.getFullYear()); // 2023

// Месяц (0-11)
console.log("Месяц:", date.getMonth()); // 9 (октябрь)

// День месяца (1-31)
console.log("День:", date.getDate()); // 25

// День недели (0-6, 0=воскресенье)
console.log("День недели:", date.getDay()); // 3 (среда)

// Время
console.log("Часы:", date.getHours()); // 15
console.log("Минуты:", date.getMinutes()); // 30
console.log("Секунды:", date.getSeconds()); // 45
console.log("Миллисекунды:", date.getMilliseconds()); // 123

// Общее время в миллисекундах
console.log("Всего миллисекунд:", date.getTime()); // Зависит от локального часового пояса конструктора
```

### 🎯 UTC методы (всемирное время)

```javascript
const date = new Date();

// Локальное время
console.log("Локальные часы:", date.getHours());

// UTC время
console.log("UTC часы:", date.getUTCHours());
console.log("UTC день:", date.getUTCDate());
console.log("UTC месяц:", date.getUTCMonth());
console.log("UTC год:", date.getUTCFullYear());
```

### 🎯 День недели в текстовом формате

```javascript
const weekDays = [
  "воскресенье",
  "понедельник",
  "вторник",
  "среда",
  "четверг",
  "пятница",
  "суббота",
];

const date = new Date();
const dayOfWeek = weekDays[date.getDay()];
console.log("Сегодня:", dayOfWeek);

const months = [
  "января",
  "февраля",
  "марта",
  "апреля",
  "мая",
  "июня",
  "июля",
  "августа",
  "сентября",
  "октября",
  "ноября",
  "декабря",
];

const month = months[date.getMonth()];
const day = date.getDate();
const year = date.getFullYear();

console.log(`Сегодня ${day} ${month} ${year} года, ${dayOfWeek}`);
```

## 📝 Установка компонентов даты

### 🎯 Основные setters

```javascript
const date = new Date();

// Изменить год
date.setFullYear(2024);
console.log("Новый год:", date.getFullYear());

// Изменить месяц (0-11)
date.setMonth(11); // Декабрь
console.log("Новый месяц:", date.getMonth());

// Изменить день
date.setDate(31);
console.log("Новый день:", date.getDate());

// Изменить время
date.setHours(23);
date.setMinutes(59);
date.setSeconds(59);
console.log(
  "Новое время:",
  `${date.getHours()}:${date.getMinutes()}:${date.getSeconds()}`,
);

// Изменить всё сразу
date.setFullYear(2025, 0, 1); // Год, месяц, день
date.setHours(0, 0, 0, 0); // Время задаётся отдельно
```

### 🎯 Последовательная установка значений

```javascript
const date = new Date();
// Метод setFullYear может принимать месяц и день сразу:
date.setFullYear(2023, 9, 25); // 25 октября 2023
date.setHours(15, 30, 0, 0);  // 15:30:00.000

console.log("Измененная дата:", date);
```

## 🎨 Форматирование дат

### 🎯 toDateString() и toTimeString()

```javascript
const date = new Date();

console.log("Дата:", date.toDateString()); // "Wed Oct 25 2023"
console.log("Время:", date.toTimeString()); // "15:30:45 GMT+0300"
console.log("Дата+время:", date.toString()); // "Wed Oct 25 2023 15:30:45 GMT+0300"
```

### 🎯 toLocaleString() - локализованный формат

```javascript
const date = new Date();

// С форматами по умолчанию
console.log("Локально:", date.toLocaleString()); // "25.10.2023, 15:30:45"
console.log("Только дата:", date.toLocaleDateString()); // "25.10.2023"
console.log("Только время:", date.toLocaleTimeString()); // "15:30:45"

// С настройками
const options = {
  weekday: "long", // "вторник"
  year: "numeric", // "2023"
  month: "long", // "октября"
  day: "numeric", // "25"
  hour: "2-digit", // "15"
  minute: "2-digit", // "30"
  second: "2-digit", // "45"
};

console.log("Полный формат:", date.toLocaleDateString("ru-RU", options));

// Короткий формат
const shortOptions = {
  year: "2-digit",
  month: "2-digit",
  day: "2-digit",
  hour: "2-digit",
  minute: "2-digit",
};

console.log("Короткий формат:", date.toLocaleString("ru-RU", shortOptions));
```

### 🎯 Ручное форматирование

```javascript
function formatDate(date) {
  const day = String(date.getDate()).padStart(2, "0");
  const month = String(date.getMonth() + 1).padStart(2, "0");
  const year = date.getFullYear();
  const hours = String(date.getHours()).padStart(2, "0");
  const minutes = String(date.getMinutes()).padStart(2, "0");
  const seconds = String(date.getSeconds()).padStart(2, "0");

  return `${day}.${month}.${year} ${hours}:${minutes}:${seconds}`;
}

const now = new Date();
console.log("Отформатировано:", formatDate(now));
// "25.10.2023 15:30:45"
```

### 🎯 Относительное время

```javascript
function relativeTime(date, now = new Date()) {
  const difference = date - now;
  if (!Number.isFinite(difference)) throw new RangeError("Некорректная дата");
  if (Math.abs(difference) < 1000) return "только что";
  const formatter = new Intl.RelativeTimeFormat("ru", { numeric: "always" });
  const units = [["day", 86400000], ["hour", 3600000], ["minute", 60000], ["second", 1000]];
  for (const [unit, size] of units) {
    if (Math.abs(difference) >= size) {
      return formatter.format(Math.trunc(difference / size), unit);
    }
  }
}

const reference = new Date("2024-03-10T12:00:00Z");
console.log(relativeTime(new Date("2024-03-10T11:55:00Z"), reference)); // 5 минут назад
console.log(relativeTime(new Date("2024-03-10T14:00:00Z"), reference)); // через 2 часа
```

Date хранит момент времени. Строка YYYY-MM-DD разбирается как UTC, а числовой конструктор new Date(year, month, day) задаёт местную дату. Локальные сутки при смене часового пояса или переходе на летнее время не всегда равны 24 часам: различайте длительность и число календарных дней.

## 🧮 Математические операции с датами

### 🎯 Сравнение дат

```javascript
const date1 = new Date(2023, 9, 25);
const date2 = new Date(2023, 9, 26);

// Сравнение через getTime()
if (date1.getTime() < date2.getTime()) {
  console.log("date1 раньше date2");
}

// Прямое сравнение работает
console.log(date1 < date2); // true
console.log(date1 > date2); // false
console.log(date1 === date2); // false (разные объекты)

// Правильное сравнение на равенство
console.log(date1.getTime() === date2.getTime()); // false
```

### 🎯 Разница между датами

```javascript
function dateDiff(date1, date2) {
  const diff = Math.abs(date1 - date2); // абсолютная разница в миллисекундах

  const milliseconds = diff % 1000; // Остаток миллисекунд; diff хранит всю длительность
  const seconds = Math.floor(diff / 1000);
  const minutes = Math.floor(seconds / 60);
  const hours = Math.floor(minutes / 60);
  const days = Math.floor(hours / 24);

  // Остатки
  const remainingHours = hours % 24;
  const remainingMinutes = minutes % 60;
  const remainingSeconds = seconds % 60;

  return {
    days,
    hours: remainingHours,
    minutes: remainingMinutes,
    seconds: remainingSeconds,
    milliseconds,
  };
}

const start = new Date(2023, 9, 25, 10, 30, 0);
const end = new Date(2023, 9, 27, 15, 45, 30);

const diff = dateDiff(start, end);
console.log("Разница:", diff);
// { days: 2, hours: 5, minutes: 15, seconds: 30, milliseconds: 0 }
```

### 🎯 Прибавление и вычитание

```javascript
function addTime(date, { days = 0, hours = 0, minutes = 0, seconds = 0 }) {
  const newDate = new Date(date);

  newDate.setDate(newDate.getDate() + days);
  newDate.setHours(newDate.getHours() + hours);
  newDate.setMinutes(newDate.getMinutes() + minutes);
  newDate.setSeconds(newDate.getSeconds() + seconds);

  return newDate;
}

const today = new Date();
const dayAfterTomorrow = addTime(today, { days: 2 });
const inOneAndHalfHour = addTime(today, { hours: 1, minutes: 30 });

console.log("Послезавтра:", dayAfterTomorrow.toLocaleDateString());
console.log("Через полтора часа:", inOneAndHalfHour.toLocaleTimeString());
```

### 🎯 Проверка високосного года

```javascript
function isLeapYear(year) {
  return (year % 4 === 0 && year % 100 !== 0) || year % 400 === 0;
}

function daysInMonth(year, month) {
  // месяц 1-12
  const daysInMonth = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];

  if (month === 2 && isLeapYear(year)) {
    return 29;
  }

  return daysInMonth[month - 1];
}

console.log("2024 високосный:", isLeapYear(2024)); // true
console.log("2023 високосный:", isLeapYear(2023)); // false
console.log("Дней в феврале 2024:", daysInMonth(2024, 2)); // 29
console.log("Дней в феврале 2023:", daysInMonth(2023, 2)); // 28
```

## ⏰ Таймеры и интервалы

### 🎯 setTimeout() - одноразовый таймер

```javascript
console.log("Начинаем...");

// Выполнится через 2 секунды
setTimeout(() => {
  console.log("Прошло 2 секунды!");
}, 2000);

console.log("Таймер установлен...");

// С отменой
const timerId = setTimeout(() => {
  console.log("Это сообщение не появится");
}, 5000);

// Отменяем через 2 секунды
setTimeout(() => {
  clearTimeout(timerId);
  console.log("Таймер отменен!");
}, 2000);
```

### 🎯 setInterval() - повторяющийся таймер

```javascript
let counter = 0;

const intervalId = setInterval(() => {
  counter++;
  console.log(`Тик ${counter}`);

  if (counter >= 5) {
    clearInterval(intervalId);
    console.log("Интервал остановлен!");
  }
}, 1000);
```

### 🎯 Часы в реальном времени

```javascript
function createClock(element) {
  function updateTime() {
    const now = new Date();
    const time = now.toLocaleTimeString("ru-RU");
    element.textContent = time;
  }

  updateTime(); // Сразу обновляем
  setInterval(updateTime, 1000); // Каждую секунду
}

// Использование (в HTML нужен элемент с id="clock")
const clockElement = document.querySelector("#clock");
if (clockElement) {
  createClock(clockElement);
}

```

## 🎯 Практические примеры

### 📅 Календарь на месяц

```javascript
function createCalendar(year, month, container) {
  const firstDay = new Date(year, month - 1, 1);
  const lastDay = new Date(year, month, 0);
  const daysInMonth = lastDay.getDate();
  const firstDayOfWeek = firstDay.getDay(); // 0=воскресенье

  const monthNames = [
    "Январь",
    "Февраль",
    "Март",
    "Апрель",
    "Май",
    "Июнь",
    "Июль",
    "Август",
    "Сентябрь",
    "Октябрь",
    "Ноябрь",
    "Декабрь",
  ];

  const calendarHtml = `
        <div class="calendar">
            <div class="calendar-header">
                <h3>${monthNames[month - 1]} ${year}</h3>
            </div>
            <div class="calendar-grid">
                <div class="calendar-day-header">Вс</div>
                <div class="calendar-day-header">Пн</div>
                <div class="calendar-day-header">Вт</div>
                <div class="calendar-day-header">Ср</div>
                <div class="calendar-day-header">Чт</div>
                <div class="calendar-day-header">Пт</div>
                <div class="calendar-day-header">Сб</div>
                ${createCalendarDays(daysInMonth, firstDayOfWeek, year, month)}
            </div>
        </div>
    `;

  container.innerHTML = calendarHtml;
}

function createCalendarDays(days, firstDayOfWeek, year, month) {
  let html = "";

  // Пустые ячейки перед первым днем
  for (let i = 0; i < firstDayOfWeek; i++) {
    html += '<div class="calendar-day empty"></div>';
  }

  // Дни месяца
  const today = new Date();
  for (let day = 1; day <= days; day++) {
    const currentDay = new Date(
      year,
      month - 1,
      day,
    );
    const isToday =
      today.getDate() === currentDay.getDate() &&
      today.getMonth() === currentDay.getMonth() &&
      today.getFullYear() === currentDay.getFullYear();

    const cssClass = isToday ? "calendar-day today" : "calendar-day";
    html += `<div class="${cssClass}">${day}</div>`;
  }

  return html;
}

// Использование
const container = document.querySelector("#calendar");
if (container) {
  const today = new Date();
  createCalendar(today.getFullYear(), today.getMonth() + 1, container);
}
```

### 🎮 Обратный отсчет

```javascript
class Countdown {
  constructor(targetDate, resultElement) {
    this.targetDate = new Date(targetDate);
    if (!Number.isFinite(this.targetDate.getTime())) throw new RangeError("Некорректная дата отсчёта");
    this.element = resultElement;
    this.interval = null;
  }

  start() {
    this.stop(); // Повторный start не создаёт второй таймер
    this.interval = setInterval(() => this.update(), 1000);
    this.update(); // Истёкший отсчёт сразу очистит установленный таймер
  }

  stop() {
    if (this.interval) {
      clearInterval(this.interval);
      this.interval = null;
    }
  }

  update() {
    const now = new Date();
    const diff = this.targetDate - now;

    if (diff <= 0) {
      this.stop();
      this.element.textContent = "Время истекло!";
      return;
    }

    const days = Math.floor(diff / (1000 * 60 * 60 * 24));
    const hours = Math.floor(
      (diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60),
    );
    const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
    const seconds = Math.floor((diff % (1000 * 60)) / 1000);

    const format = `${days}д ${hours}ч ${minutes}м ${seconds}с`;
    this.element.textContent = format;
  }
}


// Использование
const countdownElement = document.querySelector("#countdown");
if (countdownElement) {
  const countdown = new Countdown(new Date(Date.now() + 60_000), countdownElement);
  countdown.start();
}
```

### 📅 Возраст пользователя

```javascript
function calculateAge(birthDate) {
  const today = new Date();
  let birth;
  if (typeof birthDate === "string") {
    const [year, month, day] = birthDate.split("-").map(Number);
    birth = new Date(year, month - 1, day);
  } else {
    birth = new Date(birthDate);
  }

  let age = today.getFullYear() - birth.getFullYear();
  const monthDiff = today.getMonth() - birth.getMonth();

  // Если день рождения еще не прошел в этом году
  if (
    monthDiff < 0 ||
    (monthDiff === 0 && today.getDate() < birth.getDate())
  ) {
    age--;
  }

  return age;
}

// Для 29 февраля в невисокосный год здесь используется перенос Date на 1 марта.
function daysToBirthday(birthDate) {
  const today = new Date();
  today.setHours(0, 0, 0, 0); // День рождения сегодня должен дать 0
  let birthThisYear = new Date(
    today.getFullYear(),
    birthDate.getMonth(),
    birthDate.getDate(),
  );

  // Если день рождения уже прошел в этом году
  if (birthThisYear < today) {
    birthThisYear = new Date(today.getFullYear() + 1, birthDate.getMonth(), birthDate.getDate());
  }

  const utcDay = (date) => Date.UTC(date.getFullYear(), date.getMonth(), date.getDate());
  const days = Math.round((utcDay(birthThisYear) - utcDay(today)) / 86400000);

  return days;
}

// Пример использования
const birthDate = "1990-05-15";
const age = calculateAge(birthDate);
const daysToBirthdayValue = daysToBirthday(new Date(1990, 4, 15));

console.log(`Возраст: ${age} лет`);
console.log(`Дней до дня рождения: ${daysToBirthdayValue}`);
```

### 🕐 Генератор временных меток

```javascript
function timestamp(format = "полный") {
  const now = new Date();

  const year = now.getFullYear();
  const month = String(now.getMonth() + 1).padStart(2, "0");
  const day = String(now.getDate()).padStart(2, "0");
  const hours = String(now.getHours()).padStart(2, "0");
  const minutes = String(now.getMinutes()).padStart(2, "0");
  const seconds = String(now.getSeconds()).padStart(2, "0");
  const milliseconds = String(now.getMilliseconds()).padStart(3, "0");

  const formats = {
    полный: `${year}-${month}-${day} ${hours}:${minutes}:${seconds}.${milliseconds}`,
    дата: `${year}-${month}-${day}`,
    время: `${hours}:${minutes}:${seconds}`,
    имя_файла: `${year}${month}${day}_${hours}${minutes}${seconds}`,
    iso: now.toISOString(),
    timestamp: now.getTime(),
  };

  return formats[format] || formats.полный;
}

// Использование
console.log("Полный формат:", timestamp("полный"));
console.log("Только дата:", timestamp("дата"));
console.log("Только время:", timestamp("время"));
console.log("Для имени файла:", timestamp("имя_файла"));
console.log("ISO формат:", timestamp("iso"));
console.log("Timestamp:", timestamp("timestamp"));
```

## 🚨 Частые ошибки новичков

### ❌ Месяцы начинаются с 0

```javascript
// ❌ ПЛОХО - ожидаем январь, получаем февраль
const date = new Date(2023, 1, 1); // 1 февраля 2023!

// ✅ ХОРОШО - правильно используем 0-11
const correct = new Date(2023, 0, 1); // 1 января 2023
```

### ❌ Неправильное сравнение дат

```javascript
const date1 = new Date(2023, 9, 25);
const date2 = new Date(2023, 9, 25);

// ❌ ПЛОХО - сравниваем объекты, а не значения
console.log(date1 === date2); // false (разные объекты в памяти)

// ✅ ХОРОШО - сравниваем временные метки
console.log(date1.getTime() === date2.getTime()); // true
```

### ❌ Мутация оригинальной даты

```javascript
const original = new Date(2023, 9, 25);

// ❌ ПЛОХО - меняем оригинальную дату
const newDate = original;
newDate.setDate(newDate.getDate() + 1);
console.log("Оригинал изменен:", original); // 26 октября!

// ✅ ХОРОШО - создаем копию
const unchanged = new Date(2023, 9, 25);
const copy = new Date(unchanged);
copy.setDate(copy.getDate() + 1);
console.log("Оригинал цел:", unchanged); // 25 октября
console.log("Копия изменена:", copy); // 26 октября
```

### ❌ Проблема с часовыми поясами

```javascript
const date = new Date("2023-10-25"); // без времени

// Может быть проблематично из-за часовых поясов
console.log("UTC день:", date.getUTCDate()); // 25
console.log("Локальный день:", date.getDate()); // Может быть 24 или 25!

// Для местной календарной даты используйте числовой конструктор:
const localDate = new Date(2023, 9, 25);
console.log("Местный день:", localDate.getDate()); // 25
// Для момента времени указывайте Z (UTC) или смещение и выбирайте нужные getters:
const instant = new Date("2023-10-25T12:00:00Z");
console.log("UTC день:", instant.getUTCDate()); // 25
console.log("Местный день:", instant.getDate()); // Может отличаться от UTC
```

## 📚 Шпаргалка быстрых операций

| Задача            | Метод              | Пример                              |
| ----------------- | ------------------ | ----------------------------------- |
| Текущая дата      | `new Date()`       | `const now = new Date()`            |
| Из строки         | `new Date(str)`    | `new Date("2023-10-25")`            |
| Год               | `getFullYear()`    | `date.getFullYear()`                |
| Месяц             | `getMonth()`       | `date.getMonth()`                   |
| День              | `getDate()`        | `date.getDate()`                    |
| Часы              | `getHours()`       | `date.getHours()`                   |
| Время в ms        | `getTime()`        | `date.getTime()`                    |
| Форматировать     | `toLocaleString()` | `date.toLocaleString('ru-RU')`      |
| Сравнить          | `getTime()`        | `date1.getTime() < date2.getTime()` |
| Таймер            | `setTimeout()`     | `setTimeout(cb, 1000)`              |
| Интервал          | `setInterval()`    | `setInterval(cb, 1000)`             |
| Отменить таймер   | `clearTimeout()`   | `clearTimeout(id)`                  |
| Отменить интервал | `clearInterval()`  | `clearInterval(id)`                 |

## 🎮 Практика в консоли

Открой F12 и попробуй:

```javascript
// 1. Текущая дата и время
const now = new Date();
console.log("Сейчас:", now.toLocaleString("ru-RU"));

// 2. Компоненты даты
console.log("Год:", now.getFullYear());
console.log("Месяц:", now.getMonth() + 1); // +1 для нормального отображения
console.log("День:", now.getDate());
console.log("День недели:", now.getDay());
console.log("Время:", now.toLocaleTimeString("ru-RU"));

// 3. Создание даты
const birthDate = new Date(1995, 4, 15); // 15 мая 1995
console.log("ДР:", birthDate.toLocaleDateString("ru-RU"));

// 4. Возраст
function getAge(birthDate) {
  const today = new Date();
  let age = today.getFullYear() - birthDate.getFullYear();
  const monthDiff = today.getMonth() - birthDate.getMonth();
  if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birthDate.getDate())) age--;
  return age;
}
console.log("Возраст:", getAge(birthDate));

// 5. Таймер
console.log("Таймер на 3 секунды...");
setTimeout(() => {
  console.log("✅ Таймер сработал!");
}, 3000);

// 6. Интервал с остановкой
let counter = 0;
const interval = setInterval(() => {
  counter++;
  console.log(`Секунда ${counter}`);

  if (counter >= 5) {
    clearInterval(interval);
    console.log("⏹️ Интервал остановлен!");
  }
}, 1000);

// 7. Форматирование даты
function format(date) {
  return `${date.getFullYear()}-${String(date.getMonth() + 1).padStart(2, "0")}-${String(date.getDate()).padStart(2, "0")}`;
}
console.log("Форматированная дата:", format(now));

// 8. Проверка выходного
function isWeekend(date) {
  const day = date.getDay();
  return day === 0 || day === 6; // 0=воскресенье, 6=суббота
}
console.log("Сегодня выходной:", isWeekend(now) ? "Да" : "Нет");

// 9. До Нового года
function daysToNewYear() {
  const now = new Date();
  const newYear = new Date(now.getFullYear() + 1, 0, 1);
  const diff = newYear - now;
  const days = Math.floor(diff / (1000 * 60 * 60 * 24));
  return days;
}
console.log(`До Нового года: ${daysToNewYear()} дней`);

// 10. Прибавление времени
const tomorrow = new Date();
tomorrow.setDate(tomorrow.getDate() + 1);
console.log("Завтра:", tomorrow.toLocaleDateString("ru-RU"));
```

## 📝 Задания для закрепления

### Задание 1: Форматирование даты
Напиши функцию `formatDateRu(date)`, которая принимает объект `Date` и возвращает строку в формате "ДД.ММ.ГГГГ ЧЧ:ММ" (с ведущими нулями).
```javascript
formatDateRu(new Date(2023, 0, 5, 9, 3)); // "05.01.2023 09:03"
```

### Задание 2: Точный возраст
Напиши функцию `getAge(birthDateStr)`, которая принимает дату рождения в формате "ГГГГ-ММ-ДД" и возвращает полный возраст в годах (учитывая, прошёл ли уже день рождения в текущем году).

### Задание 3: Дни между датами
Напиши функцию `daysBetween(dateStr1, dateStr2)`, которая принимает две строки в формате ГГГГ-ММ-ДД и возвращает неотрицательное число полных суток между ними. Одинаковые даты дают 0.

### Задание 4: Рабочий или выходной?
Напиши функцию `isWeekend(date)`, которая принимает объект `Date` и возвращает `true`, если это суббота или воскресенье.

> 💡 Ответы к заданиям находятся в файле [answers.md](answers.md)

---

**Запомни главное:** Даты в JavaScript мощные, но требуют внимания к деталям! Месяцы начинаются с 0, сравнивайте через getTime(), и используйте `toLocaleString()` для красивого форматирования. 📅

Работа с датами - это как путешествие во времени, только в коде! ⏰🚀

## Документация

- [Date — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
- [Intl.RelativeTimeFormat — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/RelativeTimeFormat)


---

[⬅️ Предыдущая тема: События](events-js.md) | [📚 Оглавление](README.md) | [Следующая тема: Обработка ошибок ➡️](error-handling.md)
