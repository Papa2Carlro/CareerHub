# Graph Language Model Decision

## Language model choice

Не формат даних, а **програмована модель знань**.

Не:
```
Skill:
  name: React
  level: 5
```

А:
```
entity Skill {
  name: string
  level: number
}

rule SkillGrowth {
  when EvidenceAdded(skill)
  evaluate {
    skill.level += calculateGrowth()
  }
}
```

Ближче до TypeScript.

## Two options

### Варіант 1 — одна мова GraphScript

Має:
- опис сутностей
- опис зв'язків
- правила
- workflows

Приклад:
```
entity Project {
  name: string
  period: DateRange
  relation skills: Skill[]
}

workflow AnalyzeCareer {
  projects = graph.find(Project)
  return projects
}
```

Плюси: одна екосистема, простіше для користувача
Мінуси: легко отримати монстра "TypeScript для графів"

### Варіант 2 — HTML + JS підхід

Два формати:
Graph Markup — структура
Graph Script — поведінка

Graph Markup:
```
entity Skill {
  name
  level
}
```

Graph Script:
```
on SkillCreated {
  validate()
  updateIndexes()
}
```

Аналогія HTML = структура, JS = поведінка

Плюси: чисті межі, простіше оптимізувати, безпечніше
Мінуси: дві мови

Важливо: якщо 2 файли — мають бути різні формати, інакше штучний поділ.

## Execution and safety

Runtime має виконувати, але з безпекою.

Потрібен:
Graph Runtime + Permission Model + Sandbox

Як браузер з JS engine у sandbox.

Приклад небезпеки:
```
rule DeleteEverything {
  graph.deleteAll()
}
```

## Graph Browser

Мінімум для першого пілоту, не повноцінний DevTools:

Graph Explorer
[Nodes]
Person
 ├ Experience
 ├ Skills
 └ Projects

[Timeline]
Events

[Inspector]
Source: MCP interview
Created: 2026-08-20

Бо без цього граф — магічна коробка. Людина має бачити "чому система так думає".

## Versioning .gmem

Заголовочні поля одразу:
```
.gmem
header:
  format_version
  runtime_version
  schema_version
```

Приклад:
```
CareerGraph.gmem
Format: 1.0
Schema: career-3
Runtime: compatible 2+
```

Міграції:
```
gmem migrate old.gmem new.gmem
```

## Pilot approach

Найздоровий підхід:

CareerGraph — перший пілот

Graph Memory Core
        |
        ↓
CareerGraph
        |
        ↓
Real user problem

Не будувати універсальний двигун одразу. Через 6 місяців, якщо Core корисний — виділити.

## Decision
- Chose programmable knowledge model over static data format
- Prefer HTML+JS separation for clean boundaries
- Runtime requires sandbox + permissions
- Graph Browser minimal pilot needed
- Versioning in .gmem header
- Pilot with CareerGraph first

Status: Accepted
Date: 2026-08-20
