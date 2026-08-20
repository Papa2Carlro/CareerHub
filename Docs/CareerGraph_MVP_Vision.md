# Product Vision - CareerGraph MVP

CareerGraph — це не генератор резюме.
Це система управління професійною пам'яттю кандидата та адаптації позиціонування під можливості ринку.

### Main Problem

Статичне CV не відображає:
- реальний досвід;
- контекст навичок;
- докази компетенцій;
- різні можливі напрямки розвитку.

AI генератори резюме часто:
- оптимізують текст замість правди;
- створюють красивий, але слабко підтверджений профіль;
- не зберігають довготривалу професійну історію.

---

## Product Vision

CareerGraph зберігає структуровану модель професійного досвіду:

- skills;
- experience;
- projects;
- evidence;
- technologies;
- achievements;
- career goals;
- limitations.

Система повинна допомагати відповісти:

"Які мої реальні сильні сторони?"
"На які вакансії я підходжу?"
"Як правильно себе позиціонувати?"
"Яких навичок мені не вистачає?"

---

## Core MVP Flow

### 1. Користувач створює Professional Profile.

Містить:

- досвід;
- проєкти;
- навички;
- докази.

### 2. Користувач додає вакансію.

Початковий варіант:

manual paste vacancy text.

Без складних інтеграцій.

### 3. Система порівнює:

Vacancy requirements

↓

Candidate profile

↓

Match analysis

---

Результат:

Match score

Strong matches:
- навички з підтвердженням досвіду.

Weak areas:
- частковий досвід.

Missing:
- відсутні вимоги.

---

## Positioning Profiles

Один кандидат може мати декілька професійних напрямків.

Приклад:

Frontend profile:
- React
- TypeScript
- UI architecture

Backend profile:
- Node.js
- NestJS
- PostgreSQL

Fullstack profile:
- end-to-end ownership

Профіль не вигадує досвід.
Він тільки змінює акцент.

---

## MVP Non Goals

Не робити:

- автоматичну подачу заявок;
- повноцінний job board;
- генератор фейкових CV;
- складкий scraping;
- AI-first продукт.

---

## Future Extensions

Можливі:

- AI skill extraction;
- vacancy parsing;
- market analytics;
- application tracking;
- interview preparation;
- career recommendations.

---

Document created successfully. Stopping here as requested.