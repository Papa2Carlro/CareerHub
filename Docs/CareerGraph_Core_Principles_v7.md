# CareerGraph Core Principles v7

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

## Рівень 1 — Graph Memory Core MCP

Стабільний фундамент. Не знає про вакансії, CV, зарплату, LinkedIn.

Знає тільки:

- Entity
- Relation
- Event
- Evidence
- Source
- Snapshot

Приклад:

```
create_event()
{
  type: "EvidenceAdded",
  entity: "React",
  source: "user_interview"
}
```

## Рівень 2 — CareerGraph MCP

Бізнес-логіка. Агент не робить ручну агрегацію.

Замість query_graph() + 500 рядків reasoning → analyze_skill()

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

## MCP не віддає готові відповіді

Погано:

```json
{
  "answer": "Максим Senior React developer"
}
```

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

Агент сам робить висновок.

## Projection Layer

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

`generate_cv_projection()` — побудуй представлення графа під роль X, не "напиши CV".

## Повна архітектура

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
