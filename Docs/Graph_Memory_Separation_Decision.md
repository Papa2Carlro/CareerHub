# Graph Memory Separation Decision

## Problem

.cgraph format starts to conflate with CareerGraph domain. Need clean separation.

## Decision

Separate format, engine, and domain models.

```
Graph Memory Core

        |
        |
        +----------------+
        |                |
        |                |
   Storage Format     Runtime
   (.graph?)          (engine)
        |
        |
        +----------------+
                         |
                         |
                  Domain Models

                  CareerGraph
                  DocGraph
                  AssetGraph
```

## Storage Format

**`.graphmem` or `.gmem`**

Not `.cgraph` — generic format for any domain.

Structure:

```
maksym.gmem

metadata
  domain: career
  schema: career-v1

events
nodes
relations
snapshots
```

## Storage Engine

**Graph Memory Core** — event-sourced graph.

```
Event Stream

↓

Graph Projection

↓

Current State
```

Events:

- SkillCreated
- ProjectCreated
- EvidenceAdded
- DecisionRecorded
- RelationshipCreated

Graph is projection, not database.

## Domain Model

Core knows only:

- Entity
- Relation
- Event
- Property
- Evidence
- Source
- Snapshot
- Query
- Projection

CareerGraph adds:

- Skill
- Project
- Experience
- Vacancy
- Application

## One File Vault

User perception: one file = professional memory.

Internal engine optimizes like SQLite.

## Identity Snapshot

New entity:

```
2023: Frontend Developer
2026: Fullstack Engineer, Architecture Focus
2030: Engineering Lead
```

Graph History → Identity Snapshots
