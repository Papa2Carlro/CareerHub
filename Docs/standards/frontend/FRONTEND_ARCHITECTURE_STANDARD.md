# FRONTEND_ARCHITECTURE_STANDARD

## 1. Frontend Philosophy

- **Predictability over cleverness.** Архітектура має бути зрозумілою новому розробнику за 30 хвилин.
- **Feature isolation.** Кожна фіча — самодостатній модуль з чіткими межами.
- **UI is a pure function of state.** Компоненти не знають як дані приходять, лише як їх відображати.
- **Data flow is one-directional.** UI → hooks → services → API client → Backend.
- **Strict boundaries.** Шари не знають один одного вгору, лише вниз по ієрархії.

## 2. Архітектурний підхід: Feature Based Architecture

### Структура проєкту

```
src/
  app/                # Composition root, routing, providers
  features/           # Бізнес-фічі
    [feature-name]/
      components/
      hooks/
      services/
      types/
      api/
      index.ts
  components/         # Feature-agnostic UI components
  shared/             # Утиліти, константи, типи, базові стилі
  services/           # Глобальні сервіси, API клієнти, конфіг
  styles/             # Глобальні стилі, SCSS токени
```

### Відповідальність шарів

**app/**  
Точка входу. Роутинг, глобальні провайдери React Query / Zustand / Redux, ініціалізація додатку. Ніякої бізнес-логіки.

**features/**  
Серце програми. Кожна фіча повністю закрита: UI компоненти фічі, хуки для стану, сервіси для роботи з даними. Експортує публічний API через `index.ts`.

**components/**  
Переиспользувані UI компоненти без бізнес-логіки. Повинні працювати з пропсами, без доступу до stores/services. Приклад: Button, Modal, Table.

**shared/**  
Універсальні примітиви: типи, утиліти, константи, helper-и. Не знає про features/components. Може імпортуватись всюди.

**services/**  
Глобальні клієнти API, конфігурація середовища, зовнішні інтеграції. Не містить UI логіки.

**styles/**  
SCSS токени, глобальні міксини, base styles. SCSS Modules використовуються на рівні компонентів/фіч.

## 3. Dependency Rules

Напрямок імпортів строго вниз по ієрархії:

`app → features → components/shared/services`

- **shared не знає про features.** Не може імпортувати нічого з features чи components.
- **components не знають про features.** UI компоненти не містять бізнес-логіки, тільки презентацію.
- **features можуть використовувати components і shared і services.**
- **app знає про все, але нічого не реалізує.** Лише композиція.

Заборонені зв'язки:
- `shared → features/components`
- `components → features/services`
- `features/A → features/B` без публічного API

## 4. Data Flow

```
UI Component
    ↓ props / events
Custom Hook (features/*/hooks/)
    ↓
Service layer (features/*/services/ або services/)
    ↓
API Client (TanStack Query)
    ↓
Backend
```

Правила потоку:
- Компоненти лише викликають хуки.
- Хуки координують стан і викликають сервіси.
- Сервіси не знають про UI, лише про дані.
- API клієнт централізований, жодних fetch/axios в компонентах.

## 5. Rules

- **TypeScript strict mode** увімкнено. Нуль `any`, суворий typings для всього публічного API.
- **No duplicated logic.** Спільна логіка виноситься в `shared/` або сервіси. DRY обов'язково.
- **No direct API calls from components.** Тільки через хуки → сервіси → API client.
- **No giant components.** Компонент > 200 рядків — рефактор. Розбивати на sub-components.
- **Next.js/Vite.** Використовувати App Router для Next.js. Client components явно маркуються.
- **React Query/TanStack Query** для серверного стану. Zustand / Redux Toolkit для глобального клієнтського стану коли потрібно.
- **SCSS Modules** для стилів компонентів. Глобальні токени в `styles/`.
- Кожна фіча експортує публічний API в `index.ts`. Приватні модулі не експортуються.

## 6. Заборонені практики

- Імпорт `features` в `shared` / `components`.
- Бізнес-логіка всередині UI компонентів.
- Прямі fetch/axios виклики в компонентах.
- Глобальний стан для локального UI стану.
- Мішанина відповідальностей: компонент робить і UI і API і логіку.
- Використання `any`, `unknown` без явного звуження.
- Дублікати утиліт/типів між фічами.
- Імпорт всього з `features/*` без barrel `index.ts`.
- Зміна стану поза хуками/сторами.
