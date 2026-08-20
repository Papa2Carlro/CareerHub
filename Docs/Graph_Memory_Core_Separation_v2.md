# Graph Memory Core Separation v2

## Core vs Domain

Не:

```
.gmem = CareerGraph
```

А:

```
Graph Memory Core
        |
        |
        ↓

Generic Memory Format

        |
        |
        +----------------+
        |                |
        ↓                ↓

CareerGraph          DocGraph
.cgraph              .dgraph
```

`.gmem` — це низькорівневий storage/runtime формат, який належить Core.

```
SQLite engine
      |
      |
      ↓

Application database format
```

Користувач не бачить SQLite internals, але бачить свою базу.

## Фізичний файл для користувача

**Maxim.cgraph**

Можна:

- скопіювати
- зробити backup
- відправити іншому користувачу
- відкрити в CareerGraph

Ownership стає фізичним. Local-first стає реальним.

## Correction Events — Risk-based confirmation

Не жорсткий Git, не пряме редагування history.

**Human-in-the-loop correction system**:

### Low risk

```
Rename:
"React Native App" → "Mobile Application"
```

Автоматично.

### Medium risk

```
Change:
Skill depth 4 → Skill depth 2
```

Питаємо.

### High risk

```
Delete:
Commercial experience
```

Потрібне явне підтвердження.

Risk-based confirmation, як у Git:

```
git commit --amend  → безпечно
git push --force main → небезпечно
```

## MCP Flow — Structured Facts, Not Answers

Не:

```
Agent: "Знайди React досвід"
→ повертаємо текст
```

А:

```
Agent:
MCP request:
analyze_skill_depth
{
  skill_id: "react"
}

Core:
{
  "skill": "react",
  "score": 82,
  "evidence_count": 7,
  "production_projects": 3,
  "missing_context": [
    "team_size",
    "architecture_decisions"
  ]
}
```

Agent думає: "Окей, треба запитати про команду і архітектурні рішення."

### Initialize / Describe flow

```
Agent connects

↓

init()

↓

Returns:
- available tools
- graph schema
- entity types
- permissions
- response format
- limitations
```

## Query / Reasoning Interface ≠ AI Layer

Core:

- знає структуру
- шукає зв'язки
- рахує
- повертає контекст

АI:

- інтерпретує
- веде діалог
- формує рішення

Тобто:

```
Graph Core

НЕ: "Ось моя думка"
А: "Ось факти і зв'язки"
```

## Open Source Model

```
Open:

CareerGraph
- UI
- schema
- MCP server
- adapters
- workflows

Closed:

Graph Memory Core
- storage engine
- runtime
- optimization
- proprietary algorithms
```

CareerGraph — open source продукт.
Graph Memory Core — інфраструктурний moat.

Це нормальна модель.
