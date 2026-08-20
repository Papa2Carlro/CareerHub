# CareerGraph Core Principles v13

## Syntax

Hybrid TypeScript + Domain DSL

Base:
```
entity Skill { name: string; level: number }
```

Domain DSL:
```
skill React {
  maturity: advanced
  evidence: SeaRates, DocHub
}
```

## Rules

Human defines intention → AI helps generate → Compiler validates → Runtime executes

Example:
Rule generation for interview failures with human confirmation.

## Continuity
Builds on human-first AI-assisted philosophy v12 with concrete syntax and rule co-creation.

Status: Accepted
Date: 2026-08-20
