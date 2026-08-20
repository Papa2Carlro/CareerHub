# CareerGraph Core Principles v2

## 1. Атом зміни — Event

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

## 2. Merge / CRDT

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

## 3. MCP interaction model

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

## 4. Binary `.cgraph`

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