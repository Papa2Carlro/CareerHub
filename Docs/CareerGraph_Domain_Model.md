# CareerGraph Domain Model

## 1. Core Concept

Опишіть ідею:

Статичне CV показує список технологій.
CareerGraph показує:

- що людина робила;
- у якому контексті;
- наскільки глибоко;
- який був вплив;
- які рішення вона приймає.

Головний принцип:

Skill без evidence має низьку цінність.

**Це не LinkedIn із перевіркою фактів.** Кар'єрна пам'ять належить користувачеві. Система допомагає структурувати, аналізувати і краще використовувати цей досвід — але не суддіть про його валідність.

---

## 2. Main Entities

Опишіть сутності:

## Person

Центральна сутність користувача.

Містить:

- identity;
- career goals;
- professional history.

## Skill

Навичка.

Не просто тег.

Має:

- name;
- category;
- quality score;
- confidence;
- evidence references.

## Skill Evidence

Доказ використання навички.

Може містити:

- project;
- experience;
- usage context;
- depth;
- impact;
- recency.

Приклад:

**Skill:**
NestJS

**Evidence:**

- production backend;
- REST API;
- PostgreSQL;
- architecture ownership;
- deployment.

## Project

Проєкт, де був отриманий досвід.

Містить:

- purpose;
- technologies;
- role;
- timeline;
- achievements;
- constraints;
- decisions.

## Experience

Комерційний або інший досвід.

Містить:

- company/context;
- role;
- period;
- responsibilities;
- outcomes.

## Decision

Архітектурне або технічне рішення.

Містить:

- context;
- problem;
- alternatives;
- decision;
- consequences.

Приклад:

**Decision:**
Moved state management approach

**Context:**
Growing application complexity

**Alternatives:**
Redux / custom solution / query cache

**Decision:**
Selected approach

**Impact:**
Reduced duplicated logic

## Constraint

Обмеження середовища.

Приклади:

- legacy code;
- deadlines;
- compatibility requirements;
- limited resources;
- existing users.

Поясніть:

Senior-level decisions завжди мають контекст обмежень.

## Achievement

Результат роботи.

Приклади:

- delivered feature;
- improved performance;
- reduced complexity;
- automated process.

## Profile

Позиціонування кандидата.

Один Person може мати декілька профілів.

Приклади:

Frontend Engineer

Backend Engineer

Fullstack Engineer

**Profile не створює новий досвід.**
Він тільки змінює акцент.

## Vacancy

Вимоги конкретної можливості.

Містить:

- required skills;
- experience;
- constraints;
- company context.

---

## 3. Skill Quality Model

Опишіть модель оцінки якості навички.

Не використовувати тільки кількість років.

### Factors

#### Usage Context

Приклад:

Production commercial > Internal project > Open source > Large pet project > Learning

#### Recency

Оцінюється актуальність використання.

#### Depth

Рівні:

Level 1:
Used technology

Level 2:
Implemented features

Level 3:
Designed solutions

Level 4:
Made technical decisions

Level 5:
Owned direction / mentored others

#### Evidence Quality

Слабкий evidence:

"I know React"

Сильний:

"Built production React application, designed architecture, optimized performance"

#### Impact

Оцінювати:

- feature delivery;
- business impact;
- architecture improvements;
- performance improvements.

---

## 4. Skill Confidence

Додайте поняття confidence.

### Example

**High confidence:**

- multiple evidences;
- recent usage;
- production experience.

**Medium:**

- project usage;
- limited depth.

**Low:**

- learning only.

---

## 5. Matching Model

Опишіть базову ідею:

Vacancy requirements

↓

Skills

↓

Evidence

↓

Match result

### Result:

- strong matches;
- weak areas;
- missing requirements;
- confidence.

---

## 6. Professional Memory Principle

Опишіть:

CareerGraph накопичує не тільки факти, а контекст.

### Example

Не:

"Used PostgreSQL"

А:

"Used PostgreSQL in production analytics backend, designed queries and data model decisions."

---

## 7. Future Extensions

Позначте:

- AI extraction;
- career recommendations;
- market intelligence;
- interview preparation;
- application analytics.

---

## 3. Trust Model

Не:

```
Claim → Verification
```

А:

```
User Input
    ↓
Structured Memory
    ↓
Analysis / Recommendations
```

Користувач може записати:

```
Skill:
Kubernetes

Experience:
Personal project

Confidence:
Low
```

І це нормально.

CareerGraph не каже:
"Ти брешеш".

Він каже:

"Ця навичка поки має слабке підтвердження."

---

## 4. Claim + Evidence

Я б все одно залишив, але не як контроль.

Наприклад:

```
Skill:
NestJS

Claim:
Strong backend experience

Evidence:

Project:
Analytics Platform

Context:
Commercial

Depth:
Architecture decisions

Impact:
Created backend modules
```

Це допомагає людині самій зрозуміти свій рівень.

---

## 5. Exploration History — дуже цікава штука

Оце я б залишив.

Але не "невдачі", а:

Наприклад:

```
Technology:
Kubernetes

Status:
Explored

Experience:
Personal lab

Current confidence:
Low

Reason:
No production usage
```

Це корисно для:

- співбесід;
- планування розвитку;
- чесного позиціонування.

---

## 6. Skill Evolution

Тут взагалі обов'язково.

Бо кар'єра — це граф.

Не:

```
React = 5 років
```

А:

```
2021
React
Level 2

2023
React
Level 4

2026
React
Level 5
```

І можна показати:

"Ось де ти виріс".

---

## 7. AI роль

Тут я згоден на 100%.

AI не ядро.

Архітектура:

```
              AI Assistant

                    ↓

Professional Memory
                    ↓

Skills
Projects
Evidence
Decisions
Goals
```

AI тільки працює поверх.

Приклади:

### Аналіз:

> "Ти вказав React як основну навичку, але останні 3 проєкти більше показують backend профіль."

---

### Підготовка до вакансії:

> "Для цієї вакансії варто показати досвід NestJS + PostgreSQL, а не акцентувати React Native."

---

### Пошук прогалин:

> "У 8 вакансіях, які тобі цікаві, повторюється Docker. У тебе він є в досвіді, але немає окремого evidence."

---

## 8. Career Goals

Без цілі matching не має сенсу.

Єдина людина:

```
Goal:
Frontend Senior
```

Інша:

```
Goal:
Backend Node.js
```

Той самий досвід → різна рекомендація.

Додайте сутність:

```
Career Direction
```

або:

```
Career Goal
```

Вона має:

```
Target role
Preferred stack
Salary expectation
Remote preference
Industries
Learning goals
Restrictions
```

Приклад:

```
Goal:
Backend Engineer

Preferred:
- Node.js
- NestJS
- PostgreSQL

Avoid:
- pure support roles

Growth:
- distributed systems
- cloud
```