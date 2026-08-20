# Graph Language Decisions v2

## 1. Type System

Рішення: **Строга типізація + runtime validation.**

Не просто:
```
entity Skill { level: number }
```

А:
```
entity Skill {
    name: String
    level: Int
    maturity: SkillLevel
    evidence: Relation<Project>
}
```

Етап компіляції:
Graph Compiler → Type checking → Optimized schema

Runtime все одно перевіряє.

Чому: граф живий. AI agent може спробувати `Skill.level = "Senior"`, runtime має відхилити.

Мінімальна база типів:
String, Int, Float, Boolean, Date, Enum, Entity, Relation, List, Map, Optional

Не треба одразу TypeScript 2.0.

## 2. Rules vs Workflows

Розділити.

Rules — реакція на факт
```
rule SkillGrowth {
  when EvidenceAdded
  then recalculate SkillConfidence
}
```
якщо щось сталося → онови стан

Workflows — сценарій
```
workflow PrepareApplication {
  vacancy = analyzeVacancy()
  profile = selectProfile()
  generateDocuments()
}
```
зроби послідовність дій

Архітектура:
Events → Rules Engine → State changes
Workflow Engine → Orchestrates actions

## 3. Agent як частина мови

Agent — це Entity

```
Entity Agent {
  name: String
  permissions: read/propose/execute
}
```

Виконання через MCP:
Agent Definition → MCP Runtime → External AI Model

Приклад:
```
agent CareerCoach {
  permissions {
    read: [Skill, Experience]
    propose: [LearningGoal]
    execute: false
  }
}
```

Security model.

## 4. Людський контекст

Окремий шар.

Fact Layer:
```
Project: SeaRates Mobile
Technology: React Native
```

Human Context Layer:
```
Context:
First large mobile migration
Learned: technical leadership
Challenge: legacy constraints
```

Факти + контекст роблять модель людини, не CV базу.

## 5. Positioning

Не називати "нова база даних" чи "AI memory"

## Graph Memory Core

> Runtime для створення, зберігання та розвитку живих моделей знань.

Застосування:
- CareerGraph
- DocGraph
- ProjectGraph
- Agent Memory

## Decision
- Strict typing + runtime validation with minimal type set
- Rules separate from Workflows
- Agent as Entity with permissions
- Fact layer separate from Human Context layer
- Position as Graph Memory Core runtime for living knowledge models

Status: Accepted
Date: 2026-08-20
