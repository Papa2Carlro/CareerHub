# CareerHub Documentation Map

## Phase 3 — CareerHub Documentation Audit

**Goal:** Clean CareerHub documentation to keep only Product/Application layer, while Core/Language/MCP docs have been migrated to respective repositories.

**Date:** 2026-08-20

## Keep

Documents belonging to CareerHub product layer — product vision, domain models, user journey, MVP scope, UI/product decisions.

| Document | Reason |
|----------|--------|
| CareerGraph_MVP_Vision.md | Product vision and main problem statement — CareerHub specific |
| CareerGraph_User_Journey.md | User journey for CareerGraph app — product layer |
| CareerGraph_Domain_Model.md | Career domain entities (Person, Skill, Project, etc.) — CareerHub domain |
| CareerGraph_MVP_Direction_Decisions.md | MVP scope decisions — product layer |
| CareerGraph_Product_Documentation.md | Product documentation — overview, problem statement, vision |
| CareerGraph_Product_System_Model.md | Product system model, core product loop — CareerHub specific |
| CareerGraph_Core_Decisions.md | Core product decisions — onboarding, first user |
| CareerGraph_Graph_Model_Decisions.md | Graph model decisions for career domain (one graph, different subgraphs) |
| CareerGraph_Architecture_Principles.md | Product architecture principles — Professional Graph as source of truth |
| CareerGraph_MVP_Vision.md | Product vision — CareerGraph specific |
| CareerGraph_Codebase_Analysis.md | Codebase analysis — product layer implementation details |

## Move

Documents that belong to infrastructure layers and have been migrated to graph-memory-* repositories.

### graph-memory-core

| Document | Target repository |
|----------|-------------------|
| Graph_Memory_Architecture_Decision.md | graph-memory-core |
| Graph_Memory_Separation_Decision.md | graph-memory-core |
| Graph_Memory_Core_Separation_v2.md | graph-memory-core |
| Graph_Memory_Portability_Decision.md | graph-memory-core |
| Graph_Memory_Separation_Decision.md | graph-memory-core |

**Reason:** Core engine architecture, event sourcing, .gmem format, portability decisions — infrastructure layer.

### graph-memory-language

| Document | Target repository |
|----------|-------------------|
| Graph_Language_Philosophy_Decision.md | graph-memory-language |
| Graph_Language_Model_Decision.md | graph-memory-language |
| Graph_Language_Syntax_Rules_Decision.md | graph-memory-language |
| Graph_Language_Decisions_v2.md | graph-memory-language |
| Graph_Runtime_Markup_Language_Decision.md | graph-memory-language |
| Graph_Layers_Compiler_Browser_Decision.md | graph-memory-language |

**Reason:** Graph Language philosophy, syntax rules, compiler architecture, human-first language design — language layer.

### graph-memory-mcp

| Document | Target repository |
|----------|-------------------|
| Graph_Memory_Two_Level_MCP.md | graph-memory-mcp |

**Reason:** MCP protocol architecture, two-level MCP, agent permission model — MCP integration layer.

### graph-memory-spec

| Document | Target repository |
|----------|-------------------|
| CareerGraph_Schema_Architecture_Decision.md | graph-memory-spec |

**Reason:** Schema architecture decisions — spec layer.

## Archive

Historical versions or outdated documents that are superseded by newer versions.

| Document | Reason |
|----------|--------|
| CareerGraph_Core_Principles_v1.md through v14.md | Historical versions of core principles — superseded by latest v14 |
| CareerGraph_Engineering_Standards.md | Engineering standards — implementation details, may duplicate product decisions |
| CareerGraph_Repo_Structure_Proposal.md | Repo structure proposal — infrastructure layer planning, superseded |
| CareerGraph_Core_Decisions.md | Core decisions — may overlap with product decisions |

**Note:** v1-v14 series are historical versions; v14 is the latest and should be kept as reference if not already documented elsewhere.

## Recommended CareerHub Docs Structure

```
Docs/
├── Product/
│   ├── Vision/
│   │   └── MVP_Vision.md
│   ├── Domain/
│   │   ├── Domain_Model.md
│   │   ├── Vacancy_Model.md
│   │   └── User_Journey.md
│   ├── MVP/
│   │   ├── MVP_Direction_Decisions.md
│   │   └── MVP_Scope.md
│   ├── Product/
│   │   ├── Product_Documentation.md
│   │   ├── Product_System_Model.md
│   │   └── Product_Decisions.md
│   └── Architecture/
│       └── Product_Architecture_Principles.md
└── CAREERHUB_DOCUMENTATION_MAP.md
```

## Constraints Applied

- ✅ No Core engine architecture retained (event sourcing, .gmem format, etc.)
- ✅ No MCP protocol details retained
- ✅ No Graph Language/compiler design retained
- ✅ No implementation details mixed with product documentation
- ✅ Original documents preserved — no files moved or deleted, only audit performed
- ✅ CareerHub retains: Product vision, MVP scope, User journey, Career domain model, Vacancy model, Application tracking, Matching logic, UI/Product decisions, User experience

## Notes

- All documents remain in careerhub/Docs/ — no files moved
- Audit is for categorization only; no file operations performed
- Core-owned ADRs are referenced in target repositories, not in CareerHub
- CareerHub should own product layer only; infrastructure layers are in separate repositories