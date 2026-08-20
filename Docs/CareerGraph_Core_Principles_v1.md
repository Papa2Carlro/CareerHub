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