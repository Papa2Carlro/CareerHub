# CareerGraph Format Examples

**Date:** 2026-08-20  
**Owner:** careerhub  
**Purpose:** Domain-specific examples of .gmem usage for CareerGraph

This document provides CareerHub domain examples of `.gmem` file usage.
It demonstrates how CareerGraph domain concepts map to the generic `.gmem` format.

## Domain Mapping

CareerGraph domain concepts are mapped to generic `.gmem` entities and relations.

### Entities

- `Person` → Entity with properties: name, birthDate, etc.
- `Project` → Entity with properties: title, startDate, endDate, etc.
- `Technology` → Entity with properties: name, category, etc.
- `Skill` → Entity with properties: name, level, etc.
- `Evidence` → Entity with properties: type, source, date, etc.
- `Decision` → Entity with properties: summary, date, etc.

### Relations

- `PERSON_WORKED_ON` → Person → Project
- `PROJECT_USES_TECHNOLOGY` → Project → Technology
- `PERSON_HAS_SKILL` → Person → Skill
- `SKILL_EVIDENCED_BY` → Skill → Evidence
- `PERSON_MADE_DECISION` → Person → Decision
- `PROJECT_CREATED_EVIDENCE` → Project → Evidence

## Example Events

### SkillCreated

```json
{
  "event_id": "evt_001",
  "type": "EntityCreated",
  "entity_type": "Skill",
  "entity_id": "skill_123",
  "timestamp": "2026-08-20T10:00:00Z",
  "properties": {
    "name": "TypeScript",
    "level": "Advanced",
    "category": "Programming"
  }
}
```

### ProjectCreated

```json
{
  "event_id": "evt_002",
  "type": "EntityCreated",
  "entity_type": "Project",
  "entity_id": "proj_456",
  "timestamp": "2026-08-20T10:01:00Z",
  "properties": {
    "title": "Graph Memory",
    "start_date": "2026-01-01",
    "end_date": null
  }
}
```

### EvidenceAdded

```json
{
  "event_id": "evt_003",
  "type": "EventRecorded",
  "entity_type": "Evidence",
  "entity_id": "evid_789",
  "timestamp": "2026-08-20T10:02:00Z",
  "properties": {
    "type": "portfolio",
    "source": "github.com/graph-memory",
    "description": "Contribution to core engine"
  }
}
```

### DecisionRecorded

```json
{
  "event_id": "evt_004",
  "type": "EventRecorded",
  "entity_type": "Decision",
  "entity_id": "dec_101",
  "timestamp": "2026-08-20T10:03:00Z",
  "properties": {
    "summary": "Adopt Event Sourcing",
    "rationale": "Audit trail required"
  }
}
```

### RelationshipCreated

```json
{
  "event_id": "evt_005",
  "type": "RelationshipCreated",
  "from_id": "person_1",
  "to_id": "proj_456",
  "relation_type": "PERSON_WORKED_ON",
  "timestamp": "2026-08-20T10:04:00Z",
  "properties": {
    "role": "Architect",
    "hours_per_week": 20
  }
}
```

## Fact vs Context Example

### Facts

- Project entity: Graph Memory
- Technology entity: TypeScript
- Relation: PROJECT_USES_TECHNOLOGY

### Context

Human commentary separated from facts:
- Migration difficulty: high
- Leadership growth: mentored 3 engineers
- Career moment: transition to staff engineer

## Schema Definition Example

Embedded schema for CareerGraph:

```yaml
entities:
  Person:
    properties:
      name: string
      birthDate: date
  Project:
    properties:
      title: string
      startDate: date
      endDate: date?
  Technology:
    properties:
      name: string
      category: string
  Skill:
    properties:
      name: string
      level: string

relations:
  PERSON_WORKED_ON:
    from: Person
    to: Project
  PROJECT_USES_TECHNOLOGY:
    from: Project
    to: Technology
  PERSON_HAS_SKILL:
    from: Person
    to: Skill
```

## Mapping Notes

- CareerGraph domain entities map to generic `.gmem` Entity
- Domain relations map to generic `.gmem` Relation
- Domain events map to generic `.gmem` Event
- No CareerGraph concepts leak into `.gmem` format specification
- This document preserves domain examples while keeping spec generic

## References

- `graph-memory-spec/Docs/Formats/GMEM_FORMAT_OVERVIEW.md` — Generic format specification
- `Docs/Decisions/Career-Schema-Architecture.md` — Domain schema architecture
