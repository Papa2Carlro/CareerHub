# CareerGraph Core Principles v8

## Overview
Iterative principles building on v7. Schema separation finalized.

## Core Principles

1. **Core is domain-agnostic**
   - Graph Memory Core has schema engine, not domain knowledge
   - Knows Entity Types, fields, Relations, Events, validation, indexes
   - Does not interpret semantics of entities

2. **Domain schema layered on top**
   - CareerGraph domain schema defines entities and relations
   - Core + Career Schema = CareerGraph

3. **Format separation**
   - .gmem = private Graph Memory Core storage runtime format
   - .cgraph = open CareerGraph domain file format using .gmem under hood

4. **Event-sourced append-only**
   - All changes as events with provenance
   - Snapshots for fast queries
   - Change Proposal Layer with risk-based confirmation Low/Medium/High

5. **Two-level MCP**
   - Core MCP: query_graph/create_entity/add_event/create_relation/get_snapshot
   - Career MCP: match_vacancy/analyze_skill_gap/generate_profile/analyze_career_path/prepare_interview
   - MCP returns structured facts, not answers

6. **Projection Layer**
   - CV, Interview, LinkedIn reports built from graph projections
   - No duplication, projections derived

## Schema Architecture

### Graph Memory Core schema engine

EntityType definition example:

```
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

Core validates structure, builds indexes. Core does not know if Project is work, game, or document.

### Career Schema

Entities:
- Person
- Skill
- Project
- Experience
- Vacancy
- Application
- Interview
- Company

Relations:
- WORKED_ON
- HAS_SKILL
- MATCHES
- APPLIED_TO

## Composition

```
Graph Memory Core
        +
Career Schema
        =
CareerGraph
```

## Extensibility

Tomorrow DocHub can use:
```
Graph Memory Core + Documentation Schema
```
No Core changes required.

## Version History
v1 → v7 → v8 schema separation

## Decision Status
Accepted
Date: 2026-08-20
