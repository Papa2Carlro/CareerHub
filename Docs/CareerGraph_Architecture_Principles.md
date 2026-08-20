# CareerGraph Architecture Principles

## 1. Graph as Source of Truth

CareerGraph не зберігає резюме як головну сутність.

Основна модель системи — Professional Graph. Він містить:

- skills;
- experience;
- projects;
- evidence;
- decisions;
- achievements;
- constraints;
- career goals;
- preferences.

Документи є projection цього графа:

```
Professional Graph
        ↓
         CV
        ↓
  Cover Letter
        ↓
Recruiter Message
        ↓
Interview Preparation
```

Professional Graph залишається єдиною дійсною пам'яттю системи. Всі інші форми — це виведення, які можна перегенерувати в будь-який момент.

---

## 2. Projection Model

Один граф може мати багато представлень залежно від задачі.

**Frontend profile**

Акцент:

- React;
- TypeScript;
- UI architecture.

**Backend profile**

Акцент:

- Node.js;
- NestJS;
- PostgreSQL.

**Vacancy-specific CV**

Акцент:

- вимоги конкретної вакансії.

Projection не змінює факти. Вона змінює представлення.

---

## 3. AI as Interface Layer

AI не є ядром системи. AI працює поверх структурованих даних.

AI відповідає за:

- аналіз;
- рекомендації;
- генерацію представлень;
- допомогу у введенні даних.

AI не є:

- source of truth;
- сховищем професійної пам'яті;
- заміною доменної моделі.

---

## 4. MCP Integration Principle

MCP використовується як універсальний інтерфейс взаємодії AI-агентів з CareerGraph.

Архітектура:

```
AI Agent
   ↓
MCP Server (stdio)
   ↓
CareerGraph Core
   ↓
Local Storage
```

MCP може:

- читати професійний граф;
- додавати досвід;
- створювати evidence;
- аналізувати вакансії;
- генерувати представлення.

---

## 5. Interview Based Data Capture

Основний спосіб наповнення графа — розмова з AI через MCP.

Процес:

```
User describes experience
        ↓
Agent asks clarifying questions
        ↓
Extracts structured information
        ↓
Creates graph entities
```

Agent повинен уточнювати:

- технології;
- роль;
- контекст;
- масштаб;
- рішення;
- impact;
- constraints.

---

## 6. Evidence First Model

Навички мають зв'язок з evidence.

**Skill:** NestJS

**Evidence:**

- Project: Analytics Backend
- Context: Production
- Depth: Architecture decisions
- Impact: Created backend modules

Skill без evidence має меншу впевненість.

---

## 7. Skill Evolution and Snapshots

Професійний розвиток не є статичним. Система повинна підтримувати історію.

**Skill snapshot:**

```
2022:
React — Level 2

2024:
React — Level 4

2026:
React — Level 5
```

Снапшоти дозволяють аналізувати:

- розвиток;
- зміну позиціонування;
- кар'єрний прогрес.

---

## 8. Local First Privacy

CareerGraph працює за принципом: user owns data.

Основні принципи:

- дані зберігаються локально;
- cloud не є обов'язковим;
- AI provider не володіє даними;
- користувач контролює експорт.

---

## 9. Private Professional Data

Граф може містити приватний контекст.

Приклади:

- причини зміни роботи;
- результати співбесід;
- слабкі сторони;
- особисті нотатки;
- зарплатні очікування.

Ці дані можуть покращувати аналіз, але не повинні автоматично потрапляти у:

- CV;
- public profiles;
- recruiter exports.

---

## 10. Data Import and Sources

Головне джерело — user provided information.

Додаткові джерела у майбутньому:

- CV import;
- project documentation;
- Git history;
- repositories;
- job applications;
- AI conversations.

Всі джерела повинні мати зрозуміле походження.

---

## 11. Career Campaign Concept

Можлива майбутня сутність:

**Career Campaign** — певна стратегія пошуку роботи.

Може містити:

- target roles;
- target companies;
- selected profile;
- goals;
- metrics.

Не є обов'язковою частиною MVP.

---

## 12. Architecture Invariants

Незмінні правила системи:

1. Graph is source of truth.
2. Documents are projections.
3. AI assists but does not own decisions.
4. User owns professional data.
5. Evidence is more valuable than keywords.
6. Context is required for meaningful analysis.
7. MCP provides controlled AI access.
8. Privacy is default.