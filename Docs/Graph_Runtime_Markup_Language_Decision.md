# Graph Runtime + Graph Markup Language Decision

## Context
Оце зараз якраз той момент, де треба трохи загальмувати і розділити **геніальну архітектурну ідею** від **небезпечного scope creep** 😄

Аналогія з Chrome/V8 дуже влучна, але нюанс: Google спочатку не робив "власну веб-платформу". Вони взяли існуючий HTML/JS і зробили дуже швидкий engine.

У нас:

```
Graph Memory Core
        |
        |
   Runtime Engine
        |
        |
   Schema System
        |
        |
   Domain Language
```

Останній пункт — це фактично "HTML для графів".

## Що ми реально зараз винайшли
Не просто базу. Не просто формат.

А щось ближче до:

## Graph Runtime + Graph Markup Language

Умовно:

```
HTML:
описує структуру документа

Graph Language:
описує структуру знань
```

HTML:
```
<div>
  <h1>React</h1>
</div>
```

Наш формат:
```
entity Skill "React"

relation USED_IN
    Skill "React"
    Project "SeaRates"

event SkillImproved
    date 2026
```

## Важливе розділення

## 1. Graph Memory Core
Аналог V8.

Виконує:
- storage;
- events;
- snapshots;
- queries;
- schema;
- validation.

Йому байдуже, що це:
- кар'єра;
- документи;
- ассети.

## 2. Graph Markup Language
Аналог HTML.

Описує:
"Що це за граф?"

Приклад:
```
schema Career

entity Person {
    name: string
}

entity Skill {
    name: string
    level: number
}

relation HAS_SKILL {
    from Person
    to Skill
}
```

## 3. CareerGraph
Це вже "сайт".

Як браузер:
```
HTML
 |
Browser

CareerGraph Schema
 |
Graph Runtime
```

## Неймінг
Не називати HTML, бо HTML — це розмітка.

Тут ближче:
- GraphML;
- Graph Schema Language;
- Knowledge Definition Language.

## Decision
- Graph Memory Core = runtime engine, domain-agnostic
- Graph Markup Language = schema definition language for knowledge graphs
- CareerGraph = domain application built on Core + schema
- Avoid scope creep: Core stays minimal, language is separate layer

Status: Accepted
Date: 2026-08-20
