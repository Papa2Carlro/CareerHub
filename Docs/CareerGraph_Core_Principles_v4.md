# CareerGraph Core Principles v4

## Graph Memory Architecture Decision

### Storage Format ↔ Engine ↔ Domain Models

```
Graph Memory Core

        |
        |
        +----------------+
        |                |
        |                |
   Storage Format     Runtime
   (.graph?)          (engine)
        |
        |
        +----------------+
                         |
                         |
                  Domain Models

                  CareerGraph
                  DocGraph
                  AssetGraph
```

---

## 1. Event Sourced Graph (Variant C)

Так, це найкращий варіант.

Не просто:

```
Node:
React

Edges:
USED_IN
```

А:

```
Events:

SkillCreated
ProjectCreated
EvidenceAdded
DecisionRecorded
RelationshipCreated
```

Потім:

```
Event Stream

↓

Graph Projection

↓

Current State
```

Тобто граф — це не база даних. Граф — це поточне представлення історії.

### Чи engine знає домени?

**Core має бути максимально тупим.**

Ne знати:

```
Skill
Vacancy
CV
```

Інше:

```
CareerGraph:
"це система для кар'єри"
і все.
```

Краще:

```
Core знає:

Entity
Relation
Event
Property
Evidence
Source
Snapshot
Query
Projection
```

А CareerGraph додає:

```
Skill
Project
Experience
Vacancy
Application
```

### Структура сховища:

```
Graph Memory Core
        |
        |
        +-- career.graphmem
                metadata
                domain: career
                schema: career-v1

                events
                nodes
                relations
                snapshots
```

---

## 2. Формат: `.graphmem` (або `.gmem`)

Якщо назвати `.graphmem` — вже звучить як CareerGraph.

`career.graphmem` — **CareerGraph** використовує Graph Memory format.

Приклад файлу:

```
maksym.gmem

metadata:
  domain: career
  schema: career-v1

events:
  - SkillCreated
  - ProjectCreated
  - EvidenceAdded

nodes:
  - type: Skill
    name: React

relations:
  - type: USED_IN
    ...

snapshots:
  - timestamp: 2026-08-20
    state: Fullstack Engineer
```

---

## 3. Один файл (Vault)

Користувач має відчувати: "Це моя професійна пам'ять".

Не:

```
database/
  nodes/
  edges/
  cache/
```

Для нього це один vault. А всередині engine вже оптимізує.

**SQLite метафора**:

```
app.db
```

А всередині — структурні таблиці, індекси, WAL і т.д.

---

## 4. Що бачить користувач через 5 років

Правильна відповідь — **усі три режими** — бо різні моменти.

### Режим "CV"

Мені треба податись:

```
Generate Backend CV
```

### Режим "Історія"

Мені цікаво:

```
Як я виріс за 5 років?
```

### Режим "Модель себе"

Найцінніше:

```
Ось твій професійний профіль:

Strong:
Architecture
Frontend Systems

Growth:
Cloud

Market:
Backend roles currently have higher conversion

Trajectory:
Moving toward Technical Lead
```

---

## 5. Identity Snapshot

Не просто skill snapshot.

А:

```
"Який я спеціаліст у цей момент?"
```

Приклад:

```
2023:
Frontend Developer

2026:
Fullstack Engineer
Architecture Focus

2030:
Engineering Lead
```

Тобто:

```
Graph History

↓

Identity Snapshots