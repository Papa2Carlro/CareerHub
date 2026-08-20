# Graph Layers, Compiler, Browser Decision

## Layers

```
                    Graph Applications

                 CareerGraph
                 DocGraph
                 AssetGraph

                       |
                       |

              Graph Memory Language

                       |
                       |

              Graph Memory Compiler

                       |
                       |

              Graph Memory Runtime

                       |
                       |

                  .gmem binary
```

## 1. Text format + binary format

Аналогія TypeScript → JavaScript

```
.gschema / .ggraph
 |
 ↓
Graph Compiler
 |
 ↓
.gmem
```

Людина/розробник працює:
```
career.schema
entities.graph
rules.graph
```

Приклад:
```
entity Skill {
    name: string
    level: number
}

relation HAS_SKILL {
    from Person
    to Skill
}
```

Runtime працює:
```
Max.cgraph (binary)
nodes
edges
events
indexes
compiled schema
```

`.gmem` = Graph Memory compiled format
`.cgraph` = CareerGraph package

```
.cgraph
   |
   +-- schema
   |
   +-- compiled graph
   |
   +-- metadata
```

## 2. Graph Browser / Graph DevTools

Killer feature: Graph DevTools

Elements:
```
Person
 ├── Skills
 ├── Projects
 └── Experience
```

Timeline:
```
2022 Added React
2023 Production project
2025 Architecture ownership
```

Network:
```
Vacancy
 ↓
Required Skill
 ↓
Your Evidence
 ↓
Gap
```

Console:
```
graph.query(
  "find missing backend evidence"
)
```

## 3. Language and Turing complete

Schema language описує типи, зв'язки, правила. НЕ Turing complete.

Інакше schema → program, друга мова програмування.

Graph Runtime language — так, потрібна.

Близько до TypeScript + SQL + Graph Query

```
workflow AnalyzeCareer {
    skills = graph.find(Skill)
    gaps = skills.filter(s => s.confidence < 0.5)
    return gaps
}
```

```
Schema Language
        |
        ↓
Graph Programming Language
        |
        ↓
Runtime
```

## 4. Open source split

Open:
```
CareerGraph
- UI
- schemas
- domain modules
- MCP contracts
```

Possibly open:
```
Graph Language spec
```

Private:
```
Graph Runtime optimizations
Storage engine
Indexes
Execution engine
```

## 5. Graph as living environment

Graph Language → Graph Browser

Граф може бути живим середовищем.

```
Skill: React

Rule:
IF skill.used_in >= 5 projects AND production=true
THEN increase maturity
```

## Decision
- Layers separated: Applications / Language / Compiler / Runtime / .gmem
- Text .gschema/.ggraph compiled to binary .gmem
- .cgraph = CareerGraph package with schema + compiled graph + metadata
- Graph DevTools as killer feature
- Schema language non-Turing complete, runtime language is
- Open source split defined

Status: Accepted
Date: 2026-08-20
