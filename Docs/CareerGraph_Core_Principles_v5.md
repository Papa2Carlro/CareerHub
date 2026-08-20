# CareerGraph Core Principles v5

## 1. Core vs Domain Separation

```
Graph Memory Core
        |
        |
        ↓

Generic Memory Format (.gmem)

        |
        |
        +----------------+
        |                |
        ↓                ↓

CareerGraph          DocGraph
.cgraph              .dgraph
```

`.gmem` — приватний низькорівневий storage/runtime формат Graph Memory Core.

`.cgraph` — відкритий доменний формат CareerGraph, який використовує `.gmem` під капотом.

Аналогія SQLite:

```
SQLite engine
      |
      |
      ↓

Application database format
```

Користувач бачить `Maxim.cgraph`, а не внутрішні `.gmem` структури.

## 2. Фізичний файл як ownership

**Maxim.cgraph**

Можна:

- скопіювати
- зробити backup
- відправити іншому користувачу
- відкрити в CareerGraph

Ownership стає фізичним. Local-first стає реальним та відчутним.

## 3. Risk-based correction system

**Human-in-the-loop correction:**

### Low risk
```
Rename: "React Native App" → "Mobile Application"
```
Автоматично.

### Medium risk
```
Change: Skill depth 4 → Skill depth 2
```
Питаємо.

### High risk
```
Delete: Commercial experience
```
Потрібне явне підтвердження.

## 4. MCP: Structured facts, not answers

Agent запитує:

```
analyze_skill_depth { skill_id: "react" }
```

Core повертає:

```json
{
  "skill": "react",
  "score": 82,
  "evidence_count": 7,
  "production_projects": 3,
  "missing_context": ["team_size", "architecture_decisions"]
}
```

Agent сам вирішує, які питання задати.

## 5. Initialize / Describe flow для MCP

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

Агент не гадає, що повернули.

## 6. Query / Reasoning Interface ≠ AI Layer

**Core**:
- знає структуру
- шукає зв'язки
- рахує
- повертає контекст

**AI**:
- інтерпретує
- веде діалог
- формує рішення

Core каже "Ось факти і зв'язки", а не "Ось моя думка".

## 7. Open source модель

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
