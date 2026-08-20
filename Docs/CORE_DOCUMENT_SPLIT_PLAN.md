# Phase 4B — Core Document Split Plan

**Date:** 2026-08-20  
**Source:** CORE_OWNERSHIP_AUDIT_REPORT.md  
**Rule:** Не переносити файли. Тільки план.

## Split Strategy Overview

Для документів зі статусом SPLIT визначити:
Original document → Target repository → Target document name → Reason

## Documents to Split

### 1. Graph_Memory_Architecture_Decision.md

**Current location:** careerhub/Docs/Graph_Memory_Architecture_Decision.md

**Split analysis:**
- Contains generic Core concepts: graph storage, event system, snapshots, provenance, query engine, adapters, runtime, graph commit, AI rights policy, runtime engine responsibilities
- Contains CareerGraph product specifics: desktop app, MCP integration, professional graph model, career workflows, vacancy tracking, matching, exports

**Split plan:**

Original document: Graph_Memory_Architecture_Decision.md
↓
Target repository: graph-memory-core
↓
Target document name: Docs/Architecture/GMEM_ARCHITECTURE_SEPARATION.md
↓
Reason: Generic Core architecture separation, graph commit concept, runtime engine responsibilities, AI rights policy belong to Core architecture

Original document: Graph_Memory_Architecture_Decision.md
↓
Target repository: careerhub
↓
Target document name: Docs/Architecture/CAREERGRAPH_PRODUCT_ARCHITECTURE.md
↓
Reason: CareerGraph product layer definition, desktop app, career workflows, vacancy tracking, matching, exports belong to careerhub domain

### 2. Graph_Memory_Core_Separation_v2.md

**Current location:** careerhub/Docs/Graph_Memory_Core_Separation_v2.md

**Split analysis:**
- Contains generic Core concepts: .gmem as generic storage/runtime format, Core vs Domain separation, Generic Memory Format, correction events risk-based, MCP flow structured facts
- Contains CareerHub domain examples: Maxim.cgraph physical file, CareerGraph/DocGraph examples

**Split plan:**

Original document: Graph_Memory_Core_Separation_v2.md
↓
Target repository: graph-memory-core
↓
Target document name: Docs/Architecture/CORE_DOMAIN_SEPARATION.md
↓
Reason: Generic Core vs Domain separation, .gmem generic format ownership, correction events risk-based system, MCP structured facts flow are Core-level

Original document: Graph_Memory_Core_Separation_v2.md
↓
Target repository: careerhub
↓
Target document name: Docs/Architecture/CAREERGRAPH_DOMAIN_OWNERSHIP.md
↓
Reason: Physical file ownership examples (Maxim.cgraph), local-first CareerGraph specifics belong to careerhub

### 3. Graph_Memory_Portability_Decision.md

**Current location:** careerhub/Docs/Graph_Memory_Portability_Decision.md

**Split analysis:**
- Contains generic Core concepts: portability between installations, AI agent portability via MCP contract, .cgraph not API contract, storage format vs interaction protocol separation
- Contains CareerHub domain examples: Max.cgraph file examples, CareerGraph Specification vs Implementation

**Split plan:**

Original document: Graph_Memory_Portability_Decision.md
↓
Target repository: graph-memory-core
↓
Target document name: Docs/Storage/PORTABILITY_REQUIREMENTS.md
↓
Reason: Generic portability requirements, MCP contract portability, format vs protocol separation are Core storage concerns (ADR-006)

Original document: Graph_Memory_Portability_Decision.md
↓
Target repository: careerhub
↓
Target document name: Docs/Architecture/CAREERGRAPH_PORTABILITY_MODEL.md
↓
Reason: Max.cgraph examples, CareerGraph Specification vs Implementation belong to careerhub domain

### 4. Graph_Memory_Separation_Decision.md

**Current location:** careerhub/Docs/Graph_Memory_Separation_Decision.md

**Split analysis:**
- Contains generic Core concepts: format/engine/domain separation, storage format .gmem, storage engine event-sourced graph, Event Stream → Graph Projection → Current State, Core generic entities
- Contains CareerHub domain examples: Domain Model with Skill/Project/Experience/Vacancy/Application

**Split plan:**

Original document: Graph_Memory_Separation_Decision.md
↓
Target repository: graph-memory-core
↓
Target document name: Docs/Architecture/FORMAT_ENGINE_DOMAIN_SEPARATION.md
↓
Reason: Generic format/engine/domain separation, .gmem storage format, event-sourced engine model are Core architecture

Original document: Graph_Memory_Separation_Decision.md
↓
Target repository: careerhub
↓
Target document name: Docs/Architecture/CAREER_DOMAIN_SEPARATION.md
↓
Reason: CareerGraph domain model (Skill, Project, Experience, Vacancy, Application) belongs to careerhub

### 5. Graph_Runtime_Markup_Language_Decision.md

**Current location:** careerhub/Docs/Graph_Runtime_Markup_Language_Decision.md

**Split analysis:**
- Contains generic Core concepts: Graph Memory Core runtime engine responsibilities (storage, events, snapshots, queries, schema, validation)
- Contains language/spec concepts: Graph Markup Language analogy to HTML, schema definition examples
- Contains CareerHub domain examples: Career schema example

**Split plan:**

Original document: Graph_Runtime_Markup_Language_Decision.md
↓
Target repository: graph-memory-core
↓
Target document name: Docs/Architecture/RUNTIME_ENGINE_RESPONSIBILITIES.md
↓
Reason: Graph Memory Core runtime engine responsibilities are Core-level

Original document: Graph_Runtime_Markup_Language_Decision.md
↓
Target repository: graph-memory-language
↓
Target document name: Docs/Philosophy/GRAPH_MARKUP_LANGUAGE_CONCEPT.md
↓
Reason: Graph Markup Language concept, schema language design belongs to language repo

Original document: Graph_Runtime_Markup_Language_Decision.md
↓
Target repository: careerhub
↓
Target document name: Docs/Architecture/CAREERGRAPH_SCHEMA_EXAMPLE.md
↓
Reason: Career schema example belongs to careerhub

## Special Case: Graph_Memory_Two_Level_MCP.md

**Current location:** careerhub/Docs/Graph_Memory_Two_Level_MCP.md

**Ownership check:**
- Describes two-level MCP architecture: Core tools (query_graph, create_entity, add_event, create_relation, get_snapshot) vs Domain tools (match_vacancy, analyze_skill_gap)
- Core level knows only Entity/Relation/Event/Evidence/Source/Snapshot
- Domain level is CareerGraph specific

**Decision:**

Original document: Graph_Memory_Two_Level_MCP.md
↓
Target repository: graph-memory-mcp
↓
Target document name: Docs/Protocol/TWO_LEVEL_MCP_ARCHITECTURE.md
↓
Reason: MCP protocol architecture is owned by graph-memory-mcp repo, not graph-memory-core. Core tools specification belongs to MCP protocol layer. CareerGraph specific tools remain in careerhub.

## Summary Table

| Original document | Target repository | Target document name | Reason |
|---|---|---|---|
| Graph_Memory_Architecture_Decision.md | graph-memory-core | Docs/Architecture/GMEM_ARCHITECTURE_SEPARATION.md | Generic Core architecture, graph commit |
| Graph_Memory_Architecture_Decision.md | careerhub | Docs/Architecture/CAREERGRAPH_PRODUCT_ARCHITECTURE.md | CareerGraph product layer |
| Graph_Memory_Core_Separation_v2.md | graph-memory-core | Docs/Architecture/CORE_DOMAIN_SEPARATION.md | Core vs Domain, .gmem generic, correction events |
| Graph_Memory_Core_Separation_v2.md | careerhub | Docs/Architecture/CAREERGRAPH_DOMAIN_OWNERSHIP.md | Physical file examples |
| Graph_Memory_Portability_Decision.md | graph-memory-core | Docs/Storage/PORTABILITY_REQUIREMENTS.md | Generic portability requirements |
| Graph_Memory_Portability_Decision.md | careerhub | Docs/Architecture/CAREERGRAPH_PORTABILITY_MODEL.md | Domain examples |
| Graph_Memory_Separation_Decision.md | graph-memory-core | Docs/Architecture/FORMAT_ENGINE_DOMAIN_SEPARATION.md | Format/engine separation |
| Graph_Memory_Separation_Decision.md | careerhub | Docs/Architecture/CAREER_DOMAIN_SEPARATION.md | CareerGraph domain model |
| Graph_Runtime_Markup_Language_Decision.md | graph-memory-core | Docs/Architecture/RUNTIME_ENGINE_RESPONSIBILITIES.md | Runtime engine responsibilities |
| Graph_Runtime_Markup_Language_Decision.md | graph-memory-language | Docs/Philosophy/GRAPH_MARKUP_LANGUAGE_CONCEPT.md | Markup language concept |
| Graph_Runtime_Markup_Language_Decision.md | careerhub | Docs/Architecture/CAREERGRAPH_SCHEMA_EXAMPLE.md | Career schema example |
| Graph_Memory_Two_Level_MCP.md | graph-memory-mcp | Docs/Protocol/TWO_LEVEL_MCP_ARCHITECTURE.md | MCP protocol architecture |

## Notes

- No files moved yet — plan only
- Existing documents not modified
- Core already has: CORE_ARCHITECTURE.md, RUNTIME_MODEL.md, GMEM_STORAGE_MODEL.md, SNAPSHOT_AND_COMMIT_MODEL.md, DATA_PROVENANCE.md, EVENT_SOURCING_MODEL.md
- Avoid duplication with existing Core docs
- Graph_Memory_Two_Level_MCP.md belongs to graph-memory-mcp, not graph-memory-core

**Owner:** careerhub  
**Next:** Phase 4B migration execution
