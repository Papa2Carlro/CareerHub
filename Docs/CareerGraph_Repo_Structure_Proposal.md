# CareerGraph Repo & Package Structure Proposal

## V8 Analogy Correction

V8 is not a separate business product sold by Google. It exists as critical infrastructure inside the ecosystem:
- Chrome
- Chromium
- Node.js
- many other runtimes

Google does not earn directly from V8, but from products around it.

Analogy for us:

```
Graph Memory Core
        |
        |
        ↓

Infrastructure layer

        |
        |
        +----------------+
        |                |
        ↓                ↓

CareerGraph          Enterprise Graph Apps
(Open Source)        (Commercial)
```

Core can remain private engine. Money comes from:
- enterprise licenses
- integrations
- managed solutions
- special runtimes
- corporate memory systems

At start, do not think about monetization. Task now is to prove CareerGraph is needed.

---

## Repository / Package Map

Do not call everything "Graph Memory" to leave space for brand.

### 1. Core Engine

**Repo:** `graph-memory-core`
Purpose:
- storage engine
- event sourcing
- graph runtime
- snapshots
- provenance
- queries
- migrations

Internal package:
- `@gmem/core` or `@gmem/runtime`

### 2. Graph Language

**Repo:** `graph-memory-language`
Contains:
- parser
- AST
- compiler
- type checker

Packages:
- `@gmem/parser`
- `@gmem/compiler`
- `@gmem/types`

### 3. Graph CLI

**Repo:** `graph-memory-cli`
Commands:
- `gmem init`
- `gmem build`
- `gmem migrate`
- `gmem inspect`
- `gmem diff`

Package:
- `@gmem/cli`

### 4. Graph DevTools

**Repo:** `graph-memory-devtools`
Functions:
- graph explorer
- event timeline
- schema inspector
- runtime debugger

Package:
- `@gmem/devtools`

### 5. MCP Server

**Repo:** `graph-memory-mcp`
Package:
- `@gmem/mcp`

### 6. CareerGraph

Open-source product:
**Repo:** `careergraph`
Package: `@careergraph/app`

Structure:
```
careergraph
├── desktop
├── schema
├── mcp-tools
├── importers
├── projections
└── workflows
```

### 7. CareerGraph schema

**Repo:** `careergraph-schema`
Package: `@careergraph/schema`

Entities:
- Person
- Skill
- Project
- Experience
- Vacancy
- Application
- Interview

### 8. Importers

Future:
`careergraph-importers`
Packages:
- `@careergraph/github`
- `@careergraph/linkedin`
- `@careergraph/resume`

---

## Overall picture

```
                    CareerGraph

                         |
                         |
                  @careergraph/*

                         |
                         |

                 Graph Memory Core

                         |
                         |

                  @gmem/*
```

---

## Core event model

Question: Is Core event-only?

Hybrid approach:

**User/Data mutations:** EVENT ONLY
**Internal optimizations:** DIRECT MUTATIONS ALLOWED

Externally:
```
SkillUpdated event
```

Internally:
runtime can optimize indexes directly without forcing 500 events replay.

---

## Future spec repo

`graph-memory-spec`
Future standard:
- format
- protocol
- schema
- MCP contract

---

## Start set

```
graph-memory-core        🔒
graph-memory-language    🔒
graph-memory-mcp         🔒
graph-memory-cli         🔒
careergraph              🌍
careergraph-schema       🌍
```

Start with these six.

Note: Do not finalize format name `.gmem` until first prototype. Name is good but avoid tying brand to technical layer too early.
