# CareerGraph Core Principles v6

## 1. Переносимість файлу між інсталяціями CareerGraph

**Max.cgraph**

Можна:

- скопіювати
- відкрити на іншому компі
- імпортувати
- зробити backup

Це головна цінність local-first.

Фізичний файл = ownership.

## 2. Переносимість між AI агентами — через MCP контракт

```
Сьогодні:
ChatGPT
   |
   MCP
   |
CareerGraph

Завтра:
Claude
   |
   MCP
   |
CareerGraph
```

Для CareerGraph це однаково.

Агент не знає де файл, який формат, яка база, який engine.

Він знає:

```
get_profile()
analyze_skill()
find_evidence()
create_proposal()
```

## 3. .cgraph не повинен бути API контрактом

`.cgraph` — це storage format

`MCP` — це interaction protocol

Не прив'язувати API до storage.

## 4. Specification vs Implementation

```
CareerGraph Specification (open)
        |
        |
        ↓

.cgraph domain format

        |
        |
        ↓

Graph Memory Core (closed implementation)
```

Відкрите:

- які сутності існують
- які зв'язки
- як описується професійна пам'ять
- MCP контракт

Закрите:

- як швидко воно працює
- індекси
- оптимізації
- алгоритми
- storage engine

## 5. Аналогії

### HTML vs Browser Engine

```
HTML
  |
  ↓
Browser Engine
```

HTML відкритий. Blink/WebKit закриті.

### Git

```
Git repository format
        |
        ↓
Git implementation
```

Формат і engine не одне й те саме.

## 6. Підсумок архітектури

```
Користувач
    |
    ↓
Max.cgraph (file)
    |
    ↓
.cgraph domain format (open spec)
    |
    ↓
Graph Memory Core storage engine (.gmem) (closed)
    |
    ↓
MCP protocol (open spec)
    |
    ↓
AI Agents (ChatGPT, Claude, Cursor...)
```

Користувач володіє файлом.
Агенти взаємодіють через MCP.
Core оптимізує storage.
