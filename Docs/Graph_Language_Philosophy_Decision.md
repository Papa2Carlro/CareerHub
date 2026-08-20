# Graph Language Philosophy Decision

## Graph Language is human-first, AI-assisted.

Не:
> "Мова для AI, людина ніколи її не бачить"
і не:
> "Мова тільки для програмістів"

А:
> Людина може описувати і розуміти власну модель знань. AI допомагає створювати, пояснювати і перевіряти її.

## Architecture

```
              Human

                |
                |
          Graph Language
                |
                |
        Graph Compiler
                |
                |
          Graph Runtime
                |
                |
              .gmem

                ↑

             AI Agent

     generate / explain / validate
```

AI тут як Copilot для мови.

Людина пише:
```
entity Project {
    name: string
}
```

AI пропонує:
> У тебе є Skill entities, але Project не має relation HAS_SKILL. Додати?

Але не робить мовчки.

## Why human-first matters

Бо інакше втрачається головна ідея:
**користувач володіє своєю моделлю.**

Не:
"AI знає мене"

А:
"Я маю модель себе, AI допомагає з нею працювати".

## Analogies

### HTML
Людина може написати:
```
<div>Hello</div>
```
Але браузер може згенерувати.

### Graph Language
Людина може написати:
```
entity Skill {
    name: string
}
```

А агент може сказати:
> Я з твоєї розмови зрозумів, що тобі потрібна така сутність. Створити?

## What this means for CareerGraph

Перший користувач взагалі може ніколи не бачити Graph Language.

Його шлях:
```
CareerGraph UI
↓
MCP Interview
↓
AI Agent
↓
Graph Language generation
↓
Compiler
↓
Graph Runtime
↓
.cgraph
```

А розробник може:
```
edit career.schema
```
і отримати кастомний CareerGraph.

## Decision
- Graph Language human-first, AI-assisted
- User owns model, AI assists
- AI proposes, never silent changes
- First user may never see language, developer can edit schema
- Human can understand and audit own knowledge model

Status: Accepted
Date: 2026-08-20
