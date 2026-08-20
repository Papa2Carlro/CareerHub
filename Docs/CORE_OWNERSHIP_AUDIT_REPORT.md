# Phase 4B — Core Ownership Audit Report

**Date:** 2026-08-20  
**Scope:** careerhub/Docs → graph-memory-core ownership audit  
**Rule:** Не переносити файли. Тільки аудит.

## Audit Criteria

- **KEEP IN CAREERHUB**: Contains CareerHub entities, domain-specific concepts, product decisions
- **MOVE TO GRAPH-MEMORY-CORE**: Contains generic core concepts: storage, events, snapshots, provenance, runtime, architecture
- **SPLIT**: Mixes generic core concepts with CareerHub domain examples
- **ARCHIVE**: Deprecated, superseded, or duplicate

## Findings

### Graph_Memory_*

#### Document: Graph_Memory_Architecture_Decision.md
**Current purpose:** High-level separation Product/CareerGraph vs Core/Graph Memory Core, graph commit concept
**Detected ownership:** SPLIT
**Action:** SPLIT
**Reason:** Contains generic Core concepts (graph storage, event system, snapshots, provenance, query engine, adapters, runtime, graph commit) + CareerGraph product layer specifics. Core concepts already covered in graph-memory-core/Docs/Architecture/CORE_ARCHITECTURE.md. Product layer belongs to careerhub.

#### Document: Graph_Memory_Core_Separation_v2.md
**Current purpose:** Core vs Domain separation, .gmem as generic format, physical file ownership, correction events risk-based, MCP flow
**Detected ownership:** SPLIT
**Action:** SPLIT
**Reason:** Mixes generic Core architecture (.gmem generic storage/runtime) with CareerGraph domain examples (Maxim.cgraph). Correction events risk-based is generic Core concern. MCP flow with structured facts is Core-level. Domain mapping belongs to careerhub.

#### Document: Graph_Memory_Portability_Decision.md
**Current purpose:** File portability between installations, AI agent portability via MCP, .cgraph not API contract, spec vs implementation
**Detected ownership:** SPLIT
**Action:** SPLIT
**Reason:** Portability concepts are generic Core (ADR-006). CareerHub file examples (Max.cgraph) and spec vs implementation discussion mixes generic Core with domain. Core portability already documented in spec.

#### Document: Graph_Memory_Separation_Decision.md
**Current purpose:** Format/engine/domain separation, .graphmem/.gmem generic format, storage engine event-sourced graph, domain model
**Detected ownership:** SPLIT
**Action:** SPLIT
**Reason:** Generic Core separation concepts (Storage Format, Storage Engine, Event Stream → Graph Projection → Current State) belong to Core. Domain Model section mixes CareerGraph entities (Skill, Project, Experience, Vacancy) with generic Core entities. Duplicates spec ADRs.

#### Document: Graph_Memory_Two_Level_MCP.md
**Current purpose:** Two-level MCP architecture: Core tools vs Domain tools
**Detected ownership:** MOVE TO GRAPH-MEMORY-CORE
**Action:** MOVE TO GRAPH-MEMORY-CORE
**Reason:** Describes generic Core MCP layer (query_graph, create_entity, add_event, create_relation, get_snapshot) and domain separation principle. Generic Core MCP design belongs to Core. CareerGraph specific tools belong to careerhub.

#### Document: Graph_Runtime_Markup_Language_Decision.md
**Current purpose:** Graph Runtime + Graph Markup Language decision, runtime engine vs markup language analogy
**Detected ownership:** SPLIT
**Action:** SPLIT
**Reason:** Graph Memory Core runtime engine concepts (storage, events, snapshots, queries, schema, validation) are generic Core. Graph Markup Language and schema Career example belongs to language/spec. Mixes Core/runtime with language concepts.

### Core_*

#### Document: CareerGraph_Core_Decisions.md
**Current purpose:** Primary user, onboarding, core entity graph, failed applications
**Detected ownership:** KEEP IN CAREERHUB
**Action:** KEEP IN CAREERHUB
**Reason:** Entirely CareerHub product decisions: job seeker user, CV onboarding, Professional Graph as CareerGraph core entity, failed applications tracking. No generic Core concepts.

#### Document: CareerGraph_Core_Principles_v1.md — CareerGraph_Core_Principles_v14.md
**Current purpose:** Iterative career principles documentation
**Detected ownership:** KEEP IN CAREERHUB
**Action:** KEEP IN CAREERHUB
**Reason:** Domain-specific career principles, all CareerHub product. No generic Core storage/runtime concepts.

### Architecture_*

#### Document: CareerGraph_Architecture_Principles.md
**Current purpose:** Graph as source of truth, projection model, AI as interface, MCP integration
**Detected ownership:** KEEP IN CAREERHUB
**Action:** KEEP IN CAREERHUB
**Reason:** Professional Graph concepts, CV projection, AI interface for CareerGraph, MCP for CareerGraph. Generic architectural patterns but applied to Career domain.

#### Document: CareerGraph_Schema_Architecture_Decision.md
**Current purpose:** Career schema architecture decision
**Detected ownership:** KEEP IN CAREERHUB
**Action:** KEEP IN CAREERHUB
**Reason:** Domain-specific schema for CareerGraph. Already split to careerhub/Docs/Decisions/Career-Schema-Architecture.md. Spec generic schema separate.

### Storage_*/Snapshot_*/Runtime_*/Provenance_*

**No direct matches found** in careerhub/Docs root. Relevant docs exist in subfolders but outside audit scope.

## Existing graph-memory-core Documentation

Current Core docs:
- `Docs/Architecture/CORE_ARCHITECTURE.md`
- `Docs/Architecture/RUNTIME_MODEL.md`
- `Docs/Storage/GMEM_STORAGE_MODEL.md`
- `Docs/Snapshots/SNAPSHOT_AND_COMMIT_MODEL.md`
- `Docs/Provenance/DATA_PROVENANCE.md`
- `Docs/Events/EVENT_SOURCING_MODEL.md`

**Duplicate risk:** Graph_Memory_* docs duplicate Core concepts already covered above.

## Summary Table

| Document | Current purpose | Detected ownership | Action | Reason |
|---|---|---|---|---|
| Graph_Memory_Architecture_Decision.md | Product/Core separation, graph commit | SPLIT | SPLIT | Mixes generic Core + CareerGraph product |
| Graph_Memory_Core_Separation_v2.md | Core vs Domain, .gmem generic, correction events | SPLIT | SPLIT | Generic Core + CareerGraph domain examples |
| Graph_Memory_Portability_Decision.md | File/agent portability, .cgraph contract | SPLIT | SPLIT | Generic portability + CareerHub examples |
| Graph_Memory_Separation_Decision.md | Format/engine/domain separation | SPLIT | SPLIT | Generic Core + CareerGraph domain model |
| Graph_Memory_Two_Level_MCP.md | Two-level MCP architecture | MOVE TO GRAPH-MEMORY-CORE | MOVE TO GRAPH-MEMORY-CORE | Generic Core MCP layer description |
| Graph_Runtime_Markup_Language_Decision.md | Runtime + markup language | SPLIT | SPLIT | Core runtime + language concepts |
| CareerGraph_Core_Decisions.md | User, onboarding, core entity | KEEP IN CAREERHUB | KEEP IN CAREERHUB | Pure CareerHub product |
| CareerGraph_Core_Principles_v1-v14.md | Career principles iterations | KEEP IN CAREERHUB | KEEP IN CAREERHUB | Domain-specific |
| CareerGraph_Architecture_Principles.md | Graph source of truth, projections | KEEP IN CAREERHUB | KEEP IN CAREERHUB | CareerGraph architecture |
| CareerGraph_Schema_Architecture_Decision.md | Career schema | KEEP IN CAREERHUB | KEEP IN CAREERHUB | Domain schema |

## Recommendations

1. **Do not move files yet** — audit complete, Phase 4B preparation done
2. **Graph_Memory_Two_Level_MCP.md** is strongest candidate for MOVE TO GRAPH-MEMORY-CORE
3. **Graph_Memory_* docs** require SPLIT; generic parts should be moved/archived in Core, domain parts kept in careerhub
4. **No duplication** should be introduced; Core already has architecture/storage/snapshot/provenance/events docs
5. **Next phase:** Physical migration of agreed documents with ownership boundaries respected

**Owner:** careerhub  
**Next:** Phase 4B migration planning
