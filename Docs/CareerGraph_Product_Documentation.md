# CareerGraph — Початкова продуктова документація

## 1. Overview

**CareerGraph** — система управління професійним профілем та прийняття кар'єрних рішень.

Не AI генератор резюме, а платформа для збереження правдивої структурованої моделі кандидата та адаптації подачі під різні ринки.

**Ключова цінність:** зберігати професійну пам'ять у вигляді структурованих даних, а не документів. Допомагати відповідати на питання про підходящі вакансії, позиціонування, розвиток навичок та ринкові перспективи.

**Цільова аудиторія (відкрите питання):** активні job seekers, професіонали в IT, люди в процесі кар'єрного переходу.

---

## 2. Problem Statement

Поточні інструменти:
- CV/резюме — статичний документ, який важко адаптувати під різні вакансії
- AI генератори резюме — створюють «красивий текст», але не зберігають правдиву модель досвіду
- Таблиці/Notion — неструктуровані, без зв'язку між навичками, досвідом та вакансіями

**Проблеми:**
- Втрата контексту досвіду при перетворенні personal/project experience в commercial
- Відсутність структурованої моделі для порівняння з вакансіями
- Неможливість аналізу ринку на основі власних даних
- Ручне позиціонування під кожну вакансію без системної підтримки

---

## 3. Vision

Створити систему, яка:
1. Зберігає повну професійну пам'ять кандидата у структурованих даних
2. Порівнює цю модель з реальними вакансіями з ринку
3. Допомагає обирати релевантне позиціонування під кожну вакансію
4. Аналізує власну статистику пошуку та ринкові тренди

**Результат для користувача:** усвідомлене управління кар'єрою на основі фактів, а не інтуїції.

---

## 4. Core Principles

### 4.1. Правда над красою
Створити систему, яка зберігає правдиву модель кандидата і допомагає адаптувати подачу під різні ринки. Не генерувати красиве CV, а працювати з реальними даними.

### 4.2. Structured data over documents
Ядро системи — структуровані дані, правила, докази, аналітика. AI — допоміжний шар, не ядро.

AI може:
- аналізувати опис вакансії
- витягувати skills
- пропонувати позиціонування
- допомагати писати текст

AI НЕ є ядром системи.

### 4.3. Evidence-based skills
Кожен skill повинен мати контекст та докази, а не просто існувати як рядок.

Приклад:
- Skill: Go
- Type: Personal project experience
- Evidence: backend projects, API, PostgreSQL, Docker

Не можна автоматично перетворювати personal experience у commercial experience.

### 4.4. Профілі замість одного CV
Один кандидат має різні професійні профілі для різних ринків/напрямів.

### 4.5. Аналітика пошуку
Система повинна давати зворотний зв'язок на основі реальних відгуків і відповідей.

---

## 5. Main Entities

### 5.1. Professional Memory

Система зберігає:

- **Skills** — з типом досвіду, рівнем, контекстом
- **Experience** — комерційний досвід з проектами, зонами відповідальності
- **Projects** — pet-проєкти, open source, дослідження
- **Evidence** — конкретні докази навичок (код, продукти, досягнення)
- **Achievements** — вимірювані результати
- **Technologies** — стек технологій з контекстом використання
- **Career goals** — бажані напрямки розвитку, обмеження
- **Limitations** — що не цікавить / не підходить

Кожен skill має:
- назва
- тип досвіду (commercial, personal project, hobby, learning)
- рівень / confidence
- evidence references
- дата останнього використання

**Відкритий пункт:** моделювання зв'язків між skills та experience.

### 5.2. Vacancy Intelligence

Система отримує вакансії з:
- DOU RSS
- Djinni RSS
- Browser import extension
- Manual import

Для кожної вакансії зберігається:
- title
- company
- description
- required skills
- seniority
- salary
- location
- source
- date
- (відкритий пункт: обробка обов'язкових vs бажаних навичок)

### 5.3. Matching Engine

Порівнює вакансію з профілем кандидата.

**Результат:**
- Match score: 0-100%
- Strong matches: список співпадінь з вагами
- Missing: критичні відсутні навички
- Risk: overqualified, wrong positioning, географія тощо

**Відкритий пункт:** алгоритм ваг для різних типів досвіду (commercial vs personal). Як рахувати score.

### 5.4. Positioning Profiles

Один кандидат може мати різні професійні профілі.

Приклади:
- Senior Frontend Engineer
- Fullstack TypeScript Engineer
- Go Backend Transition
- Python Fullstack Developer
- DefTech / Maps Engineer

Система повинна вибирати найбільш релевантний профіль під вакансію.

Кожен профіль:
- набір skills/experience/technologies
- ключові досягнення під цей фокус
- відповідна подача

**Відкритий пункт:** механізм створення/редагування профілів. Чи автоматичний вибір чи ручний.

### 5.5. Application Tracking

Трекінг:
- вакансія
- дата відгуку
- CV version / positioning profile використаний
- cover letter
- статус
- відповідь
- співбесіди
- причина відмови

Мета: отримати власну аналітику пошуку.

### 5.6. Market Intelligence

На основі зібраних вакансій і власної статистики:

Показувати:
- які напрямки ростуть
- де найбільший match
- де найбільша конкуренція
- де найбільший шанс отримати відповідь

Приклад:
- Senior Frontend: high volume, high competition
- DefTech Maps: lower volume, higher personal fit

**Відкритий пункт:** джерела даних для аналізу конкуренції. Як визначати «шанс отримати відповідь».

---

## 6. MVP Scope

### 6.1. Платформа
Desktop application: Tauri + React + TypeScript
Storage: SQLite

### 6.2. Архітектура та код стайл

**Принципи архітектури:**
- **Local-first** — core workflows працюють офлайн, без хмари
- **Language-agnostic core** — UI адаптер, домен в Python worker
- **Closed core / open contracts** — ядро закрите, контракти між шарами відкриті
- **Deny-by-default** — жодних зовнішніх залежностей без явного дозволу

**Python domain SoT:**
- `career-memory-mcp` — Python domain source of truth
- Доменні сутності: Professional Memory, Vacancy Intelligence, Matching Engine, Analytics
- DDL / міграції SQLite — тільки в Python
- Tauri Rust — тонкий фасад, викликає worker JSON-RPC

**SQLite SoT деталі:**
- БД: `.dochub/workspace.sqlite` або аналог для CareerGraph
- WAL journal mode + foreign_keys ON + busy_timeout 30s
- Міграції схеми реалізуються в Python (`schema_python.rs` перевіряє актуальність)
- Імпорт з JSON якщо потрібно, потім DB стає SoT
- Саморемонт даних: очистка bare subtask ids, мета-флаги міграцій
- Конкурентні писарі: UI, CLI, MCP, worker — всі працюють з однією БД через прагми

**Frontend code style (канон):**

*Prettier*
```js
semi: true, tabWidth: 2, useTabs: false, singleQuote: false
trailingComma: "es5", printWidth: 120
```

*Структура компонента — одна папка = один компонент*
```
components/Profile/Skills/
  Skills.tsx
  Skills.module.scss
  index.ts
```

*SCSS modules*
- Файл: `ComponentName.module.scss`
- Root клас PascalCase: `.Skills`, `.VacancyCard`
- BEM: `.Skills__item`, `.Skills__item-title`
- Модифікатори: `&.active`, `&.primary`
- Змінні з abstracts

*classnames/bind*
```tsx
import classNames from "classnames/bind";
import scss from "./Skills.module.scss";
const cn = classNames.bind(scss);
cn("Skills__item", { active })
```

*TypeScript/React*
- Функціональні компоненти, named export
- Props тип поруч
- View UI state — view-scoped Zustand factory + Provider (ADR 0007 pattern)
- Domain data — React hooks, не дублювати в Zustand

*Імпорти*
1. React / зовнішні
2. Внутрішні абсолютні
3. Відносні
4. SCSS module

*Іменування*
- Компонент/папка: PascalCase
- Хук: useSomething.ts
- SCSS partial: _name.scss
- CSS module: Name.module.scss

### 6.3. Backend Rust архітектура

**Local-first Tauri + React + TypeScript**
Core workflows працюють офлайн. Rust бекенд — тонкий RPC фасад, доменна логіка в Python worker через JSON-RPC.

**Структура бекенду (канон Doc-Hub):**
- `src-tauri/src/lib.rs` — точка входу Tauri, ініціалізація плагінів та реєстр `invoke_handler` команд
- `src-tauri/src/commands/mod.rs` — поверхневий шар команд, реекспорт доменів:
  `agents_pack`, `code_health`, `docs`, `extension_wasm`, `host_env`, `host_viewer`, `planning`, `repo_map`, `unity`, `debug_trace`, `workspace`, `mcp_tunnel`, `tunnel_cli`
- `src-tauri/src/commands/planning/mod.rs` — Tauri-видимі команди планування, реекспорт підмодулів та `planning_unwatch_db/planning_watch_db`

**Planning домен:**
- `src-tauri/src/planning/mod.rs` — публічний API для планування: `tasks`, `epics`, `milestones`, `adrs`, `roadmaps`, `shape`, `blast`, `confidence`, `stop`, `debt`, `friction`, `orbit`, `briefcase`, `capsule`, `pilot`, `ritual`, `questions`, `glossary`, `achievements`, `trail`, `fence`, `health`, `export`, `watch`
- Використовує `db` підмодуль `rusqlite` та Python-домен SoT
- Worker/lease модель для безпечних змін стану: `worker_board.rs`, `worker_epics.rs`, `worker_milestones.rs`, `worker_closeout.rs`

**SQLite SoT та конкурентний доступ:**
- `src-tauri/src/planning/db/connection.rs` — `open_db(workspace)`
- Прагми для локальної багатокористувацької роботи:
  ```sql
  PRAGMA foreign_keys = ON;
  PRAGMA journal_mode = WAL;
  PRAGMA busy_timeout = 30000;
  ```
- `WORKSPACE_DB_BUSY_TIMEOUT_MS = 30_000` — очікування при блокуванні іншим писарем
- Маппінг помилок busy/locked в зрозумілий hint:
  `Board DB busy (.dochub/workspace.sqlite): another writer (UI/CLI/MCP/worker) holds a lock — retry in a moment`
- WAL + busy_timeout = конкурентний локальний доступ UI/CLI/MCP/worker
- Міграції схеми, `schema_is_current`, `migrate_schema`, `cleanup_bare_subtask_ids_if_needed`

**Структура lib.rs:**
- `mod` декларації: `agents_pack`, `code_health`, `commands`, `consent_registry`, `constellation`, `docs`, `extension_registry`, `extension_wasm`, `host_viewer`, `launcher_db`, `planning`, `repo_map`, `shell`, `stack_profile`, `unity_bridge`, `visibility_fence`, `debug_trace`, `worker_client`, `workspace`
- `manage(RunningProcesses)`, `manage(ScriptsWatcher)`, `manage(PlanningWatcher)`
- `invoke_handler` реєструє всі команди: `repos_*`, `constellation_*`, `extension_*`, `license_*`, `consent_*`, `workspace_health_check`, `docs_*`, `code_health_*`, `planning_*`, `debug_trace_*`, `unity_*`, `run_command*`, `mcp_tunnel_*`

**Патерни для CareerGraph:**
- Tauri бекенд як тонкий RPC-шар над SQLite SoT
- Доменні сутності реалізуються в Rust `planning/db/*` і Python-домені `career-memory-mcp`
- Розділення команд на модулі: `commands/planning/*` → `planning/*` → `planning/db/*`
- Worker/lease для безпечних змін
- `mod.rs` реекспортує публічний API, уникаючи прямих залежностей

### 6.4. Модулі MVP

1. **Profile Manager**
   - CRUD для Skills, Experience, Projects, Evidence, Achievements
   - Тип досвіду для кожного skill
   - Зв'язки Evidence → Skill

2. **Vacancy Importer**
   - Manual import вакансії
   - RSS import з DOU, Djinni (відкритий пункт: формат парсингу)
   - Збереження структури вакансії

3. **Matching Engine**
   - Базове порівняння вакансії з профілем
   - Match score
   - Strong matches / Missing / Risk

4. **CV Profiles**
   - Створення кількох positioning profiles
   - Прив'язка skills/experience до профілю

5. **Application Tracker**
   - Збереження відгуків, статусів
   - Базова аналітика

6. **Analytics Dashboard**
   - Особиста статистика по відгуках
   - Match distribution по вакансіях

### 6.5. Відкриті питання MVP
- Чи потрібна підтримка AI для парсингу вакансій на MVP?
- Формат зберігання evidence
- Як моделювати seniority
- Мова інтерфейсу

---

## 7. Future Extensions

- Browser import extension для автоматичного збору вакансій
- Інтеграція з LinkedIn / GitHub для імпорту досвіду (відкрите питання: конфіденційність)
- Експорт CV версій під профілі
- Розширена аналітика ринку
- Спільні профілі / менторський режим
- Інтеграція з тестами навичок

---

## 8. Non-goals

- **Не є AI генератором резюме.** Не створюємо «красиві» тексти як основну функцію.
- Не є автоматичним подавачем заявок на вакансії.
- Не є job board.
- Не замінює професійного кар'єрного консультанта.
- Не гарантує працевлаштування.

**Фокус:** системне управління професійною пам'яттю та дані для прийняття рішень.

---

*Документ створено: 2026-08-19*
*Статус: Draft — початкова продуктова концепція*
*Наступні кроки: погодження концепції, уточнення моделі даних, прототип*
