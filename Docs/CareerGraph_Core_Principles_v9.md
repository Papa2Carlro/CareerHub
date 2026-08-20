# CareerGraph Core Principles v9

## Overview
Загальмувати і розділити геніальну архітектурну ідею від scope creep. Аналогія Chrome/V8.

## Architecture Layers

```
Graph Memory Core
        |
   Runtime Engine
        |
   Schema System
        |
   Domain Language
```

## What we invented

Не просто базу, не просто формат.
Graph Runtime + Graph Markup Language.

```
HTML: описує структуру документа
Graph Language: описує структуру знань
```

Приклад Graph Language:
```
entity Skill "React"

relation USED_IN
    Skill "React"
    Project "SeaRates"

event SkillImproved
    date 2026
```

## Separation

### 1. Graph Memory Core
Аналог V8.

Виконує:
- storage
- events
- snapshots
- queries
- schema
- validation

Байдуже до домену: кар'єра, документи, ассети.

### 2. Graph Markup Language
Аналог HTML.

Описує "Що це за граф?"

Приклад:
```
schema Career

entity Person {
    name: string
}

entity Skill {
    name: string
    level: number
}

relation HAS_SKILL {
    from Person
    to Skill
}
```

### 3. CareerGraph
"Сайт" як browser.

```
HTML
 |
Browser

CareerGraph Schema
 |
Graph Runtime
```

## Naming
Не HTML. Ближче:
- GraphML
- Graph Schema Language
- Knowledge Definition Language

## Principles continuity
- Core domain-agnostic with schema engine
- Domain schema layered
- .gmem private, .cgraph domain
- Event-sourced append-only
- Two-level MCP
- Projection Layer

## Scope guardrails
- Core stays minimal runtime
- Language separate layer
- No universal graph for all humanity, scope to knowledge graph runtime + schema

Status: Accepted
Date: 2026-08-20
