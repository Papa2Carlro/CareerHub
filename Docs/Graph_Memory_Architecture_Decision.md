# Graph Memory Architecture Decision

## Product layer

### CareerGraph
Open source:

- desktop app;
- MCP integration;
- professional graph model;
- career workflows;
- vacancy tracking;
- matching;
- exports.

---

## Core layer

### Graph Memory Core
Private infrastructure:

- graph storage;
- event system;
- snapshots;
- provenance;
- query engine;
- adapters;
- runtime.

---
І це дуже схоже на модель:

```
Open source client

+
Private intelligence engine
```
Тобто ти не продаєш "ще один CV генератор".

---

## По пункту 1 — Git-подібна історія
Тут я думаю ми однозначно залишаємо.

Бо твій формат сам просить цього.

Я б навіть ввів поняття:

## Graph Commit
Не як Git commit, а як snapshot checkpoint.

Наприклад:

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
Тоді можна:

```
graph diff

Before:
Frontend focus

After:
Fullstack focus
```
Це дуже сильна фіча для career evolution.

---

## По пункту 2 — права AI
Оце я б зробив через policy.

Наприклад:

```
Interaction Mode

Conservative

AI:
- read
- suggest
- ask questions

User approval required

Balanced

AI:
- create drafts
- update low-risk data

Autonomous

AI:
- execute predefined operations
```
Тобто не зашиваємо одну поведінку.

---

## По пункту 3 — runtime
Тут я б не поспішав, але концептуально він потрібен.

Не:

```
library functions
```
А:

```
Graph Runtime
```
Бо він відповідає за:

- events;
- validation;
- permissions;
- queries;
- projections.
Приблизно:

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

## І тут вилізає дуже цікава штука.
Твій CareerGraph може бути першим реальним тестом для Core.

Тобто:

1. Робиш Core тільки під CareerGraph.
2. В процесі бачиш, які абстракції реально повторюються.
3. Тільки потім виділяєш.
Не навпаки.
