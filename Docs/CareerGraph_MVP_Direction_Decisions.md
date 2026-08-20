# CareerGraph — MVP Direction Decisions

## 1. Перший користувач: Dogfood first

Рішення:

> CareerGraph v0.x створюється спочатку для власного використання.

Це правильно.

Причина:

Ти зараз маєш ідеальний тестовий сценарій:

- активний пошук роботи;
- багато вакансій;
- багато відгуків;
- реальна потреба;
- реальні результати.

Тобто замість:

"давайте уявимо, що користувачеві треба"

маємо:

"мені треба це завтра".

Це найкращий спосіб валідації.

---

## 2. Graph UI не в MVP

Рішення:

Professional Graph — це **внутрішня модель**, а не головний інтерфейс.

Перші екрани:

```
CareerGraph

├── Profile
├── Projects
├── Skills
├── Vacancies
├── Applications
├── Insights
└── Settings
```

А Graph View — пізніше:

```
Explore Graph

Skill
 |
Project
 |
Decision
 |
Achievement
```

Бо інакше є ризик зробити красиву карту, яку ніхто не відкриває.

---

## 3. Storage

Тут треба уточнити.

Відповідь:

> В, але якщо правильно зрозумів, то D

Мається на увазі:

- не просто SQLite;
- а щось ближче до graph storage.

Рішення:

## Концептуально:
Так, це Graph.

## Технічно MVP:
Не треба одразу Graph DB.

Архітектура:

```
Local Files / SQLite

        +

Graph domain layer
```

Тобто:

```
CareerGraph Core

        |
        |

Graph Model

        |
        |

Storage Adapter

        |
        |

SQLite / Files
```

Чому:

Якщо ми зараз візьмемо спеціальну graph database, ми можемо випадково будувати базу замість продукту. Спочатку треба перевірити модель.

---

## 4. Desktop first

Так.

Перша архітектура:

```
Tauri App

├── React UI
│
├── CareerGraph Core
│
├── Local Storage
│
└── MCP Server (stdio)
```

А вже потім:

```
Browser Extension

        ↓

CareerGraph Core
```

---

## 5. Назва

CareerGraph — залишаємо.

І мені подобається, бо назва не обмежує.

Не:

"CV AI"

Не:

"Job Finder"

Не:

"Resume Generator"

А:

Career + Graph.

Тобто:

> Граф професійної історії людини.

---

# CareerGraph v0.1

## Goal

Довести:

> Чи може structured professional graph покращити процес пошуку роботи?

---

## Milestone 1 — Build My Graph

Функції:

- створити профіль;
- імпорт CV;
- додати LinkedIn/GitHub дані;
- MCP interview;
- створення:
  - projects;
  - skills;
  - experience;
  - evidence.

Результат:

```
Мій Professional Graph
```

---

## Milestone 2 — Vacancy Analysis

Функції:

- вставити вакансію;
- зберегти;
- розібрати вимоги;
- match.

Результат:

```
Match 82%

Strong:
React
TS

Weak:
AWS

Missing:
Kubernetes
```

---

## Milestone 3 — Application Generation

Функції:

- вибрати vacancy;
- вибрати positioning;
- згенерувати:
  - CV;
  - cover letter;
  - recruiter message.

---

## Milestone 4 — Feedback Loop

Функції:

- application tracking;
- interview results;
- feedback;
- insights.