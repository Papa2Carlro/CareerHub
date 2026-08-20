# Schema Architecture Decision

## Graph Memory Core
Core не знає доменів.

Він має **schema engine**.

Його задача:

- знати, що існують Entity Types;
- знати поля;
- знати Relations;
- знати Events;
- валідовувати структуру;
- будувати індекси.

Наприклад:

```
EntityType

{
  name: "Project",

  fields:
    - name
    - created_at
    - metadata

  relations:
    - HAS_SKILL
    - HAS_EVIDENCE
}
```

Але Core не знає:

> Project — це робота, гра чи документ.

---

## Domain Schema
Вже CareerGraph додає:

```
career.schema

Entity:

Person
Skill
Project
Experience
Vacancy
Application
Interview
Company

Relations:

WORKED_ON
HAS_SKILL
MATCHES
APPLIED_TO
```

---

Тобто:

```
Graph Memory Core

        +
        
Career Schema

        =

CareerGraph
```

---

Це дає нам можливість:

Наприклад, завтра:

```
DocHub

uses:

Graph Memory Core

+

Documentation Schema
```

і Core навіть не треба міняти.

## Principles

- Core schema-agnostic, schema engine validates structure
- Domain schemas are separate declarative definitions
- Core provides Entity Types, fields, Relations, Events, indexes
- Domain provides semantics: Person, Skill, Project, Experience, Vacancy, Application, Interview, Company
- Portability: swap domain schema without touching Core
- Extensibility: DocHub, other domains reuse Core with own schema

## Decision Status
Accepted
Date: 2026-08-20
