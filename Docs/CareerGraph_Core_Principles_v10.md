# CareerGraph Core Principles v10

## Layers

```
Graph Applications
    CareerGraph / DocGraph / AssetGraph
        |
Graph Memory Language
        |
Graph Memory Compiler
        |
Graph Memory Runtime
        |
.gmem binary
```

## Format separation

`.gschema / .ggraph` → Compiler → `.gmem`

Human works with:
```
career.schema
entities.graph
rules.graph
```

Runtime works with `Max.cgraph` binary: nodes, edges, events, indexes, compiled schema

`.gmem` = Graph Memory compiled format
`.cgraph` = CareerGraph package = schema + compiled graph + metadata

## Graph Browser / DevTools

Killer feature.

Elements like Chrome DOM
Timeline like Performance
Network like Chrome Network
Console for graph.query

## Language design

Schema Language: types, relations, rules. Non-Turing complete.

Runtime Language: TypeScript + SQL + Graph Query style

```
workflow AnalyzeCareer {
    skills = graph.find(Skill)
    gaps = skills.filter(s => s.confidence < 0.5)
    return gaps
}
```

## Open source split

Open: CareerGraph UI, schemas, domain modules, MCP contracts
Possibly open: Graph Language spec
Private: Runtime optimizations, storage engine, indexes, execution engine

## Living graph

Graph as living environment with rules:
```
IF skill.used_in >= 5 projects AND production=true
THEN increase maturity
```

## Continuity
v1-v9 principles maintained with layered compiler/browser model and scope guardrails.

Status: Accepted
Date: 2026-08-20
