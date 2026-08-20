# CareerGraph Core Principles v1

## 1. `.cgraph` — власний формат, але з можливістю адаптерів
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

---

## 2. Append-only історія
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

---

## 3. Provenance обов'язково
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

---

## 4. MCP як основний interface
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
Тобто UI стає просто одним із клієнтов.

Можна мати:

- ChatGPT;
- Claude;
- Codex;
- Cursor;
- локальний агент;
- Tauri UI.
Всі говорять з одним ядром.

---

## 5. CareerGraph Core як бібліотека
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
І тут вилізла дуже цікава річ.

CareerGraph починає бути схожим на:

**Git + Knowledge Graph + MCP runtime для професійної пам'яті.**

---

## 6. Атом зміни — Event

Тут ми однозначно приходимо до B.

Не:

```
Skill.updated
```

А:

```
Event:

User added experience with Go

Context:
Personal project

Source:
MCP interview

Timestamp:
2026-08-20
```

Тобто граф — це не таблиця станів, а результат подій.

Приблизно:

```
Events

↓ replay

Current Graph State
```

Плюси:

- історія без втрати;
- rollback;
- аналіз розвитку;
- AI може бачити еволюцію.

---

## 7. Merge / CRDT

Тут я б не поспішав із повним CRDT.

Але сама ідея потрібна.

Бо джерела будуть різні:

```
                 User
                  |
                  |
CV Import ---- CareerGraph ---- MCP Agent
                  |
                  |
              GitHub Import
```

І всі можуть пропонувати зміни.

Я б зробив не "автоматичний merge", а:

### Change Proposal Layer

Наприклад:

AI:

> Я знайшов, що ти працював з PostgreSQL у 3 проектах.
Створює:

```
Proposal:

Add Evidence:
PostgreSQL

Source:
GitHub analysis

Confidence:
0.82
```

Користувач:

Accept / Edit / Reject

Після цього:

```
Event:
EvidenceAdded
```

Тобто без хаосу.

---

## 8. MCP interaction model

Оце треба окремо зафіксувати, бо це дуже важлива відмінність.

Я думав:

> агент питає граф "дай мені дані".

А у тебе:

> агент просить у графа "допоможи знайти області, де потрібне уточнення".

Тобто MCP не просто CRUD.

Він більше схожий на **reasoning support layer**.

Наприклад:

Агент:

```
analyze_profile_completeness()
```

CareerGraph:

повертає:

```
{
  "missing_context": [
    {
      "entity": "Project SeaRates",
      "missing": [
        "impact",
        "technical decisions"
      ]
    },
    {
      "skill": "React Native",
      "missing": [
        "production scale"
      ]
    }
  ]
}
```

А агент вже будує інтерв'ю:

> "Розкажи, який був масштаб SeaRates Mobile?"

Тобто:

```
CareerGraph
    |
    | gives structure gaps
    ↓
AI Agent
    |
    | conducts conversation
    ↓
User
```

Це набагато ближче до твоєї ідеї DocHub/MCP.

---

## 9. Binary `.cgraph`

Тут цікава позиція.

Я б тільки додав один нюанс.

Не робити просто:

```
careergraph.bin
```

Бо потім буде біль.

Я б розділив:

### Storage format

```
.cgraph
```

Бінарний optimized format.

### Adapter layer

```
Graph Adapter

↓

Views:

- JSON
- Markdown
- Visualization
- MCP response
- Export
```

Тобто користувач ніколи не працює напряму з форматом.