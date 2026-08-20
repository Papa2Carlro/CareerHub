# Graph Language Syntax & Rules Decision

## 1. Syntax: TypeScript + Domain DSL

Гібрид.

Базово:
```
entity Skill {
    name: string
    level: number
}
```

Доменні конструкції спеціалізовані:
```
skill React {

    maturity: advanced

    evidence:
        SeaRates
        DocHub

}
```

Не вигадувати нову мову заради нової мови.

Беремо:
- читабельність TypeScript
- доменну виразність DSL

Аналогія:
TypeScript + React JSX
JSX не замінює JS, додає доменний шар.

## 2. Rules: human + AI

Якщо тільки AI — чорна коробка.
Якщо тільки вручну — ніхто не буде писати.

Потрібно:
```
Human defines intention
        ↓
AI helps generate
        ↓
Compiler validates
        ↓
Runtime executes
```

Приклад:
Людина: "Я хочу, щоб після невдалих співбесід система створювала learning goal."

AI пропонує:
```
rule InterviewFailure {
  when Interview.status == "Rejected"
  then create LearningGoal
}
```

Людина підтверджує.

## Decision
- Syntax hybrid: TypeScript readability + domain DSL expressiveness
- Rules co-created by human intention + AI generation + compiler validation + runtime execution
- Human stays in control, AI assists

Status: Accepted
Date: 2026-08-20
