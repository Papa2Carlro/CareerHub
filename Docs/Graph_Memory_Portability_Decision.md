# Graph Memory Portability Decision

## 1. Переносимість файлу між інсталяціями CareerGraph

Так.

Приклад:

```
Max.cgraph
```

Можна:

- скопіювати
- відкрити на іншому компі
- імпортувати
- зробити backup

Це головна цінність local-first.

## 2. Переносимість між AI агентами

Теж так, але не через файл.

А через MCP контракт.

Приклад:

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

Бо агент не знає:

- де файл
- який формат
- яка база
- який engine

Він знає:

```
get_profile()
analyze_skill()
find_evidence()
create_proposal()
```

## 3. .cgraph не повинен бути API контрактом

Бо тоді ти прив'яжешся до storage.

Краще:

```
.cgraph
це storage format

MCP
це interaction protocol
```

## 4. CareerGraph Specification vs Implementation

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

Аналогія:

```
HTML
  |
  ↓
Browser Engine
```

HTML відкритий. Blink/WebKit закриті.

Або:

```
Git repository format
        |
        ↓
Git implementation
```

Формат і engine не одне й те саме.
