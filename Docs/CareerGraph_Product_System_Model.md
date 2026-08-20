# CareerGraph Product System Model

## 1. Product Vision

### Проблема

Поточний процес пошуку роботи розділений між безліччю інструментів та джерел:

- CV у різних редакціях;
- нотатками в блокнотах;
- чатами з AI без контексту;
- таблицями з відгуками;
- закладками вакансій;
- повідомленнями в месенджерах;
- несв'язаною статистикою.

Кожен інструмент тримає частину історії. Разом вони утворюють фрагментовану систему, в якій важко відповісти на прості запитання:

- до яких вакансій я вже відгукувався?
- яка версія профілю використовувалася для конкретного відгуку?
- яке позиціонування дає кращу відповідь?
- які навички підтверджені реальним досвідом, а які — лише вгадуванням?

### Рішення

CareerGraph об'єднує весь процес пошуку роботи в одну локальну систему, де професійна пам'ять, вакансії, заявки та аналітика зберігаються в єдиному контексті.

---

## 2. Core Product Loop

Система будує замкнутий цикл покращення професійної позиції:

```
Professional Profile
        ↓
Vacancy Collection
        ↓
    Matching
        ↓
Application Preparation
        ↓
Application Tracking
        ↓
    Analytics
        ↓
Profile Improvement
```

Кожен етап генерує дані, які покращують наступний. Аналітика повертається до профілю, створюючи безперервний цикл адаптації.

---

## 3. Professional Memory

CareerGraph зберігає структурований професійний профіль, а не набір окремих фактів.

### Структура профілю

- **Skills** — технічні та Soft skills
- **Experience** — історія роботи
- **Projects** — реалізовані проєкти
- **Evidence** — підтвердження навичок
- **Achievements** — результатів діяльності
- **Decisions** — архітектурних та продуктових рішень
- **Constraints** — обмежень та контексту
- **Career Goals** — цілей розвитку
- **Preferences** — уподобань щодо роботи

### Головний принцип

**Skill без контексту має низьку цінність.**

Система не зберігає відривкові описи навичок. Вона зберігає контекст, в якому ці навички застосовувалися.

**Ні:**

```
React — 5 років
```

**Так:**

```
React production experience:
- архітектурні рішення для SPA застосунку;
- оптимізація продуктивності (Core Web Vitals);
- менторство junior розробників;
- інтеграція з REST API та WebSocket.
```

---

## 4. Vacancy Intelligence

### MVP: Manual Import

На початковому етапі вакансії додаються вручну:

- вставка тексту вакансії;
- автоматичне витягування вимог;
- збереження в системі.

### Майбутнє

Подальше розширення передбачає:

- browser extension;
- інтеграції з job boards;
- автоматичний збір вакансій.

### Сущність Vacancy

- **company** — компанія;
- **role** — назва посади;
- **stack** — стек технологій;
- **requirements** — вимоги;
- **salary** — зарплатні діапазони;
- **location** — локація;
- **status** — стан обробки;
- **date** — дата публікації.

---

## 5. Matching Engine

### Принцип роботи

```
Vacancy requirements
        +
Professional Memory
        ↓
    Match Analysis
```

Система порівнює вимоги вакансії з структурованим профілем користувача.

### Результат аналізу

**Strong matches**

Навички, для яких є сильне підтвердження (evidence) у профілі.

**Partial matches**

Є досвід використання, але його глибина або актуальність недостатні для повної відповідності.

**Missing**

Вимоги, які відсутні в професійній пам'яті.

### Важливе обмеження

Matching не повинен вигадувати досвід. Система показує реальну відповідність, а не ідеалізований збіг.

---

## 6. Profile Positioning

### Множинність профілів

Одна людина може мати декілька професійних профілів. Профіль не змінює факти — він змінює акценти.

### Приклад

**Frontend Engineer**

- React;
- TypeScript;
- UI architecture;
- компонентний дизайн.

**Backend Engineer**

- Node.js;
- NestJS;
- PostgreSQL;
- API дизайн.

**Fullstack**

- end-to-end ownership;
- інтеграція фронтенду та бекенду;
- продуктова відповідальність.

Кожен профіль використовує той самий набір фактів, але організований під конкретну робочу роль.

---

## 7. AI Assistant Layer

### Роль AI

AI є допоміжним шаром, що працює поверх структурованих даних CareerGraph.

### AI допомагає

- аналізувати вакансії;
- знаходити прогалини в профілі;
- генерувати CV під конкретну вакансію;
- генерувати cover letter;
- готувати interview notes;
- рекомендувати альтернативне позиціонування.

### AI не

- створює фейковий досвід;
- є source of truth;
- замінює модель даних;
- приховує невідповідності.

AI використовує Professional Memory як контекст, але не перезаписує його.

---

## 8. Application Management

### Принцип

Кожен відгук на вакансію фіксується в системі з повним контекстом.

### Сущність Application

- **vacancy** — посилання на вакансію;
- **used profile** — який профіль був використаний;
- **date** — дата подання;
- **status** — поточний стан.

### Життєвий цикл заявки

- **Draft** — заявка готується;
- **Applied** — відгук відправлено;
- **Viewed** — вакансію переглянули;
- **Recruiter Contact** — контакт з рекрутером;
- **Interview** — співбесіда;
- **Technical Interview** — технічна співбесіда;
- **Offer** — отримано offer;
- **Rejected** — відмова;
- **Ghosted** — без відповіді.

---

## 9. Analytics

### Що вимірюється

Система збирає статистику пошуку роботи для об'єктивної оцінки ефективності різних стратегій.

### Приклади метрик

- кількість відгуків;
- response rate (відгук → перегляд);
- interview rate (відгук → співбесіда);
- offer rate (відгук → offer);
- джерела вакансій;
- ефективність профілів;
- ефективність різних позиціонувань.

### Використання

Аналітика допомагає виявляти:

- які канали дають кращий відгук;
- яке позиціонування підходить під поточний ринок;
- де є прогалини в профілі, що знижують відповідність.

---

## 10. Local First Architecture

### Принцип

CareerGraph працює локально. Дані зберігаються на пристрої користувача.

### Основи архітектури

- desktop application;
- локальна база даних;
- користувач володіє даними;
- AI provider є опціональним.

### Переваги

- **privacy** — дані не покидають пристрій без згоди;
- **control** — користувач вирішує, що і як синхронізувати;
- **offline capability** — система працює без підключення до інтернету.

---

## 11. MVP Scope

### Version 0.1 — Включити

- Professional Profile;
- Vacancy Import;
- Matching;
- Profile Positioning;
- CV generation;
- Cover letter generation;
- Application Tracker.

### Не включати в MVP

- automatic applying;
- повноцінна job board;
- complex scraping;
- social network;
- mandatory cloud account.

---

## 12. Future Extensions

### Планові напрямки розвитку

- **Browser Extension** — швидке збереження вакансій з job boards;
- **Integrations** — підключення зовнішніх сервісів;
- **Market Intelligence** — аналіз ринку вакансій;
- **Interview Preparation** — підготовка до співбесід на основі профілю та вакансії;
- **Automated Application Workflows** — автоматизація рутинних етапів подачі заявок.

---

## 13. Product Principles

- **User owns professional data.** Користувач має повний контроль над своїми даними.
- **AI assists but does not replace structure.** AI є інструментом, а не ядром системи.
- **Evidence over keywords.** Підтвердження важливіше за перерахування.
- **Context over raw skill lists.** Контекст використання навички важливіший за список.
- **Local-first privacy.** Локальне зберігання — основний принцип.
- **Continuous improvement loop.** Система створює цикл постійного вдосконалення профілю.

---

## 14. CareerGraph Core Principles v1

### 1. `.cgraph` — власний формат, але з можливістю адаптерів

Рішення:

**A — власний формат як source format.**

Але:

```
.cgraph
        ↓
Export adapters
        ↓
JSON
Markdown
CV formats
AI formats
```

Тобто JSON не є базою. Він просто один із форматів експорту.

Приклад:

```
CareerGraph

.cgraph
    graph/
    nodes/
    edges/
    snapshots/
    provenance/

export/
    cv.json
    profile.md
    linkedin.md
```

Це дуже схоже на те, як працюють компілятори:

```
Source language
       ↓
Intermediate Representation
       ↓
Different outputs
```

CareerGraph фактично стає IR для професійної інформації.

### 2. Append-only історія

Так.

Тут ми вже визначили.

Не:

```
Skill:
React

Level:
5
```

А:

```
Skill:
React

Events:

2022:
Added

2023:
Production usage

2025:
Architecture ownership

2026:
Mentoring
```

Тобто стан — це результат обчислення історії.

Приблизно:

```
Current Graph State =
Replay(all events)
```

Це дуже добре лягає на DTJ-мислення.

### 3. Provenance обов'язково

Це прям фундамент.

Кожен факт має знати:

```
WHO
WHEN
WHY
FROM WHERE
```

Наприклад:

```
Node:
  type: Skill
  name: NestJS

Created:
  source: MCP interview
  date: 2026-08-20

Modified:
  source: user correction

Evidence:
  project: Analytics Backend
```

Це вирішує проблему AI.

Бо AI може помилятися.

А система знає:

"Це не факт із повітря, це було введено користувачем під час інтерв'ю".

### 4. MCP як основний interface

Оце, думаю, найцікавіше рішення.

Не:

```
Desktop app
    |
    |
 MCP plugin
```

А:

```
              User

               |
               |

        Conversational Interface

               |
               |

          MCP Protocol

               |
               |

       CareerGraph Core

               |
               |

          .cgraph storage
```

Тобто UI стає просто одним із клієнтів.

Можна мати:

- ChatGPT;
- Claude;
- Codex;
- Cursor;
- локальний агент;
- Tauri UI.

Всі говорять з одним ядром.

### 5. CareerGraph Core як бібліотека

Так.

Я б навіть сказав:

Tauri — не продукт.

Tauri — перший клієнт.

Архітектура:

```
careergraph-core

├── Graph Engine
├── Storage Engine
├── Query Engine
├── Event System
└── Provenance

Clients:

├── Tauri Desktop
├── MCP Server
├── CLI
└── Browser Extension
```

---

CareerGraph починає бути схожим на:

**Git + Knowledge Graph + MCP runtime для професійної пам'яті.**
