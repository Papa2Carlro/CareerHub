# Graph Memory Two-Level MCP Architecture

## Дворівневий MCP API

```
                    AI Agent
                       |
                       |
                     MCP
                       |
        +--------------+--------------+
        |                             |
        ↓                             ↓

Graph Memory Tools              Domain Tools

(core layer)                   (CareerGraph layer)

query_graph()                  match_vacancy()
create_entity()                analyze_skill_gap()
add_event()                    generate_profile()
create_relation()              analyze_career_path()
get_snapshot()                 prepare_interview()
```

---

# Рівень 1 — Graph Memory Core MCP

Стабільний фундамент.

Нічого не знає про:

- вакансії
- CV
- зарплату
- LinkedIn

Знає тільки:

## Entities

```
Entity
```

## Relations

```
Relation
```

## Events

```
Event
```

## Evidence

```
Evidence
```

## Sources

```
Source
```

## Snapshots

```
Snapshot
```

Приклад:

Агент: Додай новий факт

Core:
```
create_event()
{
  type: "EvidenceAdded",
  entity: "React",
  source: "user_interview"
}
```

---

# Рівень 2 — CareerGraph MCP

Бізнес-логіка.

Агент не повинен сам робити:

```
знайти всі Skill nodes
порахувати evidence
оцінити confidence
знайти вакансію
порівняти
```

Даємо:

```
analyze_skill()
```

Core повертає:

```json
{
  "skill": "React",
  "evidence_count": 12,
  "production_projects": 5,
  "timeline": "2021-2026",
  "missing_context": [
    "team leadership",
    "architecture decisions"
  ]
}
```

Агент вже спілкується.

---

# MCP не повинен віддавати "готові відповіді"

Має віддавати **структурований контекст для reasoning**.

Погано:

```json
{
  "answer": "Максим Senior React developer"
}
```

Бо це вже думка.

Добре:

```json
{
  "experience_years": 5,
  "projects": 8,
  "production_usage": true,
  "architecture_decisions": 14,
  "mentoring": true
}
```

Агент робить висновок.

---

# Projection Layer

CareerGraph має багато представлень.

```
Graph
  ↓
Projection Engine
  ↓
CV
Interview Prep
LinkedIn
Recruiter Message
Career Report
```

MCP:

```
generate_cv_projection()
```

Не "напиши CV", а "побудуй представлення графа під роль X".

---

# Повна архітектура

```
                 AI Agents

        ChatGPT / Claude / Cursor
                    |
                    |
                  MCP

        +-----------+-----------+

        Core MCP             Career MCP

        |                       |

        +-----------+-----------+

              Graph Runtime

                    |

              .cgraph format

                    |

          Graph Memory Core
```
