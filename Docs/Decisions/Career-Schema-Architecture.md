# Career Schema Architecture

## Domain Schema
CareerGraph додає доменну схему:

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

## Composition

```
Graph Memory Core

        +
        
Career Schema

        =

CareerGraph
```

## Domain Entities

### Person
Career participant.

### Skill
Professional capability.

### Project
Work or portfolio item.

### Experience
Professional experience entry.

### Vacancy
Job opening.

### Application
Application to vacancy.

### Interview
Interview stage.

### Company
Organization.

## Relations

- WORKED_ON — Person ↔ Project
- HAS_SKILL — Person ↔ Skill / Project ↔ Skill
- MATCHES — Skill ↔ Vacancy
- APPLIED_TO — Person ↔ Vacancy

## Principles

- Domain provides semantics: Person, Skill, Project, Experience, Vacancy, Application, Interview, Company
- Domain schema is declarative definition separate from Core
- Domain schema can evolve independently of Core
- Portability: Career schema can be reused or modified

## Decision Status
Accepted
Date: 2026-08-20
Source: Split from ADR-012_Schema_Architecture_Decision.md — CareerGraph domain portion extracted
