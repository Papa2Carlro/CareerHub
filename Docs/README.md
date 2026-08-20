# CareerHub — Documentation Entry Point

Product/application repository for CareerGraph.

## Purpose

CareerHub is the product layer built on Graph Memory. It owns domain models for
careers, UI workflows, user journeys, and MVP scope. All infrastructure decisions
are owned by `graph-memory-*` repositories.

## Documentation Map

```
Docs/
├── README.md                           ← this file
├── CAREERHUB_DOCUMENTATION_MAP.md      # What stays vs moves
├── CareerGraph_Architecture_Principles.md
├── CareerGraph_Product_Documentation.md
├── CareerGraph_Product_System_Model.md
├── CareerGraph_MVP_Vision.md
├── CareerGraph_User_Journey.md
├── CareerGraph_Domain_Model.md
├── CareerGraph_MVP_Direction_Decisions.md
├── CareerGraph_Core_Decisions.md       # Product core decisions
├── CareerGraph_Graph_Model_Decisions.md
└── standards/
    ├── UI_DESIGN_SYSTEM_STANDARD.md
    ├── backend/
    └── frontend/
    └── tauri/
```

*Historical core principles files (v1-v14) are archived as they have been
migrated to the spec repositories.*

## Where to Start

| If you want to… | Read |
|---|---|
| Product vision and context | `CareerGraph_Product_Documentation.md` |
| Product system model | `CareerGraph_Product_System_Model.md` |
| MVP vision & scope | `CareerGraph_MVP_Vision.md` |
| User journey | `CareerGraph_User_Journey.md` |
| Domain model | `CareerGraph_Domain_Model.md` |
| Documentation map | `CAREERHUB_DOCUMENTATION_MAP.md` |

## Related Repositories

| Repository | Relationship |
|---|---|
| `graph-memory-spec` | ADRs and decision registry; read-only reference |
| `graph-memory-core` | Engine providing `.gmem` and event sourcing |
| `graph-memory-language` | Graph Language for authoring domain models |
| `graph-memory-mcp` | MCP tools for AI-assisted workflows |
| `graph-memory-cli` | CLI tooling |

## Source of Truth Boundaries

- CareerHub owns product vision, domain models, user journeys, UI standards,
  and MVP decisions.
- CareerHub does **not** own infrastructure architecture, file formats, event
  sourcing, or MCP protocol.
- Infrastructure decisions are sourced from `graph-memory-spec/ADRs/`.
- This README is navigation only; it introduces no new architectural decisions.