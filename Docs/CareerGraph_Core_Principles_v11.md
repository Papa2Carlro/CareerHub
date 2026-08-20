# CareerGraph Core Principles v11

## Language model

Programmable knowledge model, not static data format.

Schema + rules + workflows in one language leaning to TypeScript.

## Architecture choice

Prefer HTML+JS separation:
- Graph Markup = structure
- Graph Script = behavior

Clean boundaries, optimizable, safer.

If two files, formats must differ, otherwise artificial split.

## Runtime safety

Graph Runtime + Permission Model + Sandbox

Like browser JS engine.

## Graph Browser pilot

Minimal Graph Explorer needed:
Nodes tree, Timeline, Inspector with source and creation date.

Graph must be explainable.

## Versioning

.gmem header:
format_version
runtime_version
schema_version

Migration tool: gmem migrate old.gmem new.gmem

## Pilot focus

CareerGraph as first pilot.

Graph Memory Core → CareerGraph → Real user problem

No universal engine upfront. Validate with real use, then extract Core.

## Continuity
Maintains layers, compiler, devtools, open source split from v10 with explicit language model choice and safety.

Status: Accepted
Date: 2026-08-20
