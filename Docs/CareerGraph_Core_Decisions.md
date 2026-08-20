# CareerGraph — Core Decisions

## 1. Primary User

Перший користувач:

**активний job seeker.**

Але архітектура не обмежується ним.

Тобто:

MVP:

> "Допомогти людині знайти роботу ефективніше"

Long-term:

> "Професійна пам'ять людини протягом кар'єри"

Це правильний порядок. Не треба одразу продавати "довічну кар'єру", коли людині зараз треба пройти співбесіду в понеділок 😄

---

## 2. Onboarding

Дуже важливе рішення:

Не:

```
Create profile
100 полів
Save
```

А:

```
Collect existing data
        ↓
Build initial graph
        ↓
Interview refinement
        ↓
Continuous enrichment
```

Джерела:

- існуюче CV;
- LinkedIn;
- GitHub;
- портфоліо;
- власні документи;
- ручне введення;
- MCP interview.

Тобто перший граф будується із вже існуючих слідів.

---

## 3. Core Entity

Відповідь:

> Graph.

Це найважливіше.

Не:

```
CareerGraph = CV generator
```

А:

```
CareerGraph = Professional Graph

CV = Graph projection
```

---

## 4. Failed Applications

Залишаємо.

Я б навіть сказав — це один з найцінніших типів даних.

Бо успішний кандидат знає:

"Що я робив"

А сильний кандидат ще знає:

"Що не спрацювало".

Модель:

```
Application
    +
Outcome
    +
Feedback
    +
Learnings
```

Наприклад:

```
Interview:
Senior Frontend

Result:
Rejected

Reason:
System design

Updated insight:
Improve architecture interview preparation
```

І граф стає живим.

---

## 5. Positive + Negative Memory

Також залишаємо.

Але не називати це "weakness".

Краще:

## Skill State

Наприклад:

```
AWS

State:
Exploring

Evidence:
Personal projects

Confidence:
Low

Goal:
Production experience
```

Бо "слабкість" звучить як оцінка.

А це просто стан розвитку.

---

## 6. Dashboard

Оце вже хороший target.

Я бачу перший екран:

```
CareerGraph

Current Profile:
Fullstack Engineer

Market Match:
82%

Strong Areas:
React
TypeScript
Node.js

Growth Areas:
Cloud
System Design

Job Search:

Applications:
42

Responses:
7

Interviews:
3

Insights:

"Backend positions currently convert better"
```

---

## 7. Sync

Правильно.

Не ускладнюємо.

MVP:

```
Local SQLite
+
Export/Import
```

Потім:

```
Encrypted sync
```

---

## 8. Graph UI

Тут я би обережно.

Граф як **модель** — так.

Граф як основний UI — можливо ні.

Бо красивий node graph часто стає "вау на демо", але працювати з ним щодня незручно.

Я б:

Основний UI:

```
Profile
Projects
Skills
Applications
Insights
```

А граф:

```
Explore Mode
```

Типу:

"Покажи зв'язки між моїм React досвідом і вакансіями".

---

## 9. Career Advisor

Беремо.

Але після бази.

Спочатку:

```
Data
    ↓
Analysis
    ↓
Recommendation
```

Не:

```
AI придумав пораду
```

---

## 10. Moat

Тут погоджуюсь:

**B + C**

Professional Graph + accumulated history.

Тобто через рік:

Новий користувач:

```
Empty graph
```

Ти:

```
5 років досвіду
100 вакансій
50 matching results
20 interview outcomes
```

І це вже персональна модель.