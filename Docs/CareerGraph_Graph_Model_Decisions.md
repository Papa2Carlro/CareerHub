# CareerGraph — Graph Model Decisions

## 1. Один граф чи декілька?

Правильніше мислити не як "два графи", а як **один граф з різними доменними підграфами**.

Бо вакансія теж частина кар'єри.

```
CareerGraph

Person
 |
 |
 +----------------+
 |                |
 |                |
Professional   Career Activity
Graph          Graph

 |                |
Skills            Vacancies
Projects          Applications
Evidence          Interviews
Decisions         Outcomes
Experience        Feedback
```

Зв'язки між ними:

```
Skill: React
      |
      |
      +---- Project: SeaRates
      |
      |
      +---- Vacancy: Senior React Developer
                         |
                         |
                         +---- Application
```

Тобто:

- **Professional Graph** відповідає: "хто я як інженер?"
- **Career Activity Graph**: "що я роблю на ринку?"

І вони взаємодіють.

Це краще, ніж повністю розділити, бо тоді втрачається головна фішка:

> Моя історія + реакція ринку = наступні рішення.

---

## 2. DTJ і AI traces

Не зберігати кожну розмову в граф.

Бо буде болото:

```
User said:
...
AI said:
...
```

Через місяць там буде смітник.

### DTJ
Технічний execution trace:

```
Agent action
Tool call
Result
Decision path
```

Тобто "як працював агент".

### CareerGraph
Тільки отримані знання:

```
Created:
Project

Updated:
Skill

Added:
Evidence
```

Але можна мати посилання:

```
Evidence

source:
dtj://trace_12345
```

Тобто:

граф не зберігає весь процес, але може сказати: "звідки це взялося".

---

## 3. Manual override

Так, однозначно.

Це навіть важливий принцип.

AI не володіє моделлю. Модель належить користувачу.

Наприклад:

AI стверджує:

```
Docker:
Production experience
```

User корегує:

```
Correction:
Development only
```

Тоді в графі:

```
Skill Evidence

claim:
Docker production

status:
rejected

replacement:
Docker development
```

Не видаляти історію, а зберігати еволюцію.

Це дуже в стилі графа.

---

## 4. Imports

MCP + CV.

Але не робити імпорт як "створи мені профіль".

Краще:

```
Source
 |
Extraction
 |
Candidate entities
 |
Review
 |
Graph merge
```

Тобто:

CV не пише прямо в граф. Воно створює пропозиції.

Наприклад:

```
Found:

Skill:
NestJS

Confidence:
0.82

Add?
[Yes]
[Edit]
[No]
```

Бо інакше один кривий CV може забруднити весь граф.

---

## 5. Власний низькорівневий формат графа

JSON не підходить для knowledge graph:

- добре для API;
- погано для knowledge graph;
- погано для versioning;
- погано для великих зв'язків.

### Концептуальний формат `.cgraph`

```
GRAPH CareerGraph v1

NODE Person maxym

NODE Skill React
{
 created: 2022
 state: active
}

NODE Project SeaRates

EDGE USED_IN
Skill React
Project SeaRates

EDGE CREATED
Person maxym
Project SeaRates
```

Тобто:

- nodes;
- edges;
- attributes;
- snapshots;
- history.

### Або ближче до Git

```
.cgraph/

nodes/
edges/
snapshots/
events/
```

Тоді:

```
careergraph commit

+
careergraph diff
```

І тут DTJ ідея дуже красиво стикується.

### Уяві:

```
CareerGraph

commit 001
Added:
Project SeaRates

commit 002
Updated:
React skill

commit 003
Added:
Decision:
Module Federation
```

У тебе фактично **Git для професійної пам'яті**.