# CareerGraph Core Principles v3

## Graph Memory Architecture Decision

### Product layer

**CareerGraph** — Open source:

- desktop app;
- MCP integration;
- professional graph model;
- career workflows;
- vacancy tracking;
- matching;
- exports.

### Core layer

**Graph Memory Core** — Private infrastructure:

- graph storage;
- event system;
- snapshots;
- provenance;
- query engine;
- adapters;
- runtime.

Модель:

```
Open source client

+
Private intelligence engine
```

Тобто ти не продаєш "ще один CV генератор".

---

## 1. Git-подібна історія → Graph Commit

Тут однозначно залишаємо.

Бо твій формат сам просить цього.

Вводимо поняття:

### Graph Commit
Не як Git commit, а як snapshot checkpoint.

Приклад:

```
Commit 001

Created:
- Person
- Experience
- Skills

Commit 002

Added:
- SeaRates project
- React evidence

Commit 003

Updated:
- Backend profile
- Career goal
```

Функції:

```
graph diff

Before:
Frontend focus

After:
Fullstack focus
```

Це дуже сильна фіча для career evolution.

---

## 2. Права AI — через policy

Не зашиваємо одну поведінку.

### Interaction Mode

**Conservative**

AI:
- read
- suggest
- ask questions

User approval required

**Balanced**

AI:
- create drafts
- update low-risk data

**Autonomous**

AI:
- execute predefined operations

---

## 3. Runtime замість бібліотеки

Тут не поспішаємо, але концептуально потрібен.

Не:

```
library functions
```

А:

```
Graph Runtime
```

Відповідає за:

- events;
- validation;
- permissions;
- queries;
- projections.

Архітектура:

```
                 Clients

Desktop
MCP
CLI
Extension

                  ↓

          Graph Memory Runtime

                  ↓

              .cgraph
```

---

## 4. CareerGraph як перший тест Core

Твій CareerGraph може бути першим реальним тестом для Core.

Тобто:

1. Робиш Core тільки під CareerGraph.
2. В процесі бачиш, які абстракції реально повторюються.
3. Тільки потім виділяєш.
Не навпаки.
