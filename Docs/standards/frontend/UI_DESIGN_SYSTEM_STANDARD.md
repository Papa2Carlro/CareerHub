# UI_DESIGN_SYSTEM_STANDARD

## Принципи

- **Tokens first.** Всі візуальні значення через токени
- **Semantic colors.** Ніколи не використовувати raw кольори, тільки семантичні токени
- **Components over utility classes.** UI будується через компоненти, не через utility класи

## Design Tokens

### Токени зберігаються в `styles/tokens/`
Експортуються як SCSS змінні та JavaScript об'єкт для runtime доступу.

#### Colors
Семантичні токени, не raw HEX:

```
color-background-primary
color-background-secondary
color-text-primary
color-text-secondary
color-border-default
color-action-primary
color-action-primary-hover
color-status-success
color-status-warning
color-status-error
color-status-info
```

Заборонено використовувати raw HEX/RGB в компонентах.

#### Typography
Типографіка токенізується повністю:

```
font-family-base
font-family-mono
font-size-xs/xs/sm/md/lg/xl/2xl
font-weight-regular/medium/semibold/bold
line-height-tight/normal/loose
letter-spacing-normal/wide
```

Жодних хардкод значень `font-size`/`line-height` в компонентах.

#### Spacing
8px grid система:

```
space-0 = 0
space-1 = 4px
space-2 = 8px
space-3 = 12px
space-4 = 16px
space-5 = 24px
space-6 = 32px
space-8 = 48px
space-10 = 64px
```

Використовувати тільки токени spacing.

#### Radius
```
radius-sm = 4px
radius-md = 8px
radius-lg = 12px
radius-xl = 16px
radius-full = 9999px
```

#### Shadows
```
shadow-sm
shadow-md
shadow-lg
shadow-xl
```

Всі тіні через токени, без кастомних `box-shadow`.

## Component Contract

Базовий набір компонентів `components/ui/`. Кожен компонент має однаковий API контракт.

### Core Components

**Button**
- variants: `primary/secondary/tertiary/danger`
- sizes: `sm/md/lg`
- states: `default/hover/active/disabled/loading`
- props: `variant`, `size`, `disabled`, `loading`, `fullWidth`

**Input**
- types: `text/email/password/number`
- states: `default/focused/error/disabled`
- props: `label`, `error`, `helperText`, `leftIcon`, `rightIcon`

**Select**
- single/multi
- searchable/creatable
- props: `options`, `value`, `onChange`, `placeholder`

**Modal**
- sizes: `sm/md/lg/full`
- props: `isOpen`, `onClose`, `title`, `footer`
- Обов'язковий фокус trap, esc to close, body scroll lock

**Toast**
- types: `success/error/warning/info`
- auto dismiss, position fixed
- props: `title`, `description`, `duration`

**Tabs**
- controlled/uncontrolled
- props: `tabs`, `activeTab`, `onChange`

**Card**
- variants: `default/elevated/bordered`
- props: `header`, `footer`, `padding`

**Badge**
- variants: `default/success/warning/error/info`
- sizes: `sm/md`
- props: `variant`, `size`, `dot`

Кожен компонент:
- Поширює `data-testid` для e2e
- Має `aria-*` атрибути
- Слідує токенам
- Експортується через `components/ui/index.ts`

## Rules

- Новий UI тільки через `components/ui/`
- Компоненти не приймають raw кольори/спейсинг, тільки токени і variants
- Компоненти повинні бути accessible за замовчуванням
- Всі компоненти мають Storybook story
- Ніяких копій-paste компонентів між продуктами

## Заборонено

- **inline styles.** Всі стилі через SCSS Modules або токени
- **random colors.** Тільки семантичні токени
- **duplicate buttons.** Не створювати нові кнопки, використовувати `components/ui/Button`
- Utility класи для побудови UI
- Магічні числа в стилях

## Component Lifecycle

Статуси компонентів в дизайн-системі:

**Experimental**
- Можна використовувати тільки в експериментальних фічах
- API може змінюватись
- Потребує review від дизайн-системи

**Stable**
- Публічний API заморожений
- Гарантована підтримка
- Можна використовувати всюди

**Deprecated**
- Позначено для видалення в наступній major версії
- Не можна використовувати в новому коді
- Має міграційний guide

Кожен компонент має коментар з lifecycle статусом.

## Theme Contract

Дизайн-система підтримує декількі продукти через Theme Contract.

```
theme/
  base.tokens.json      # Базові токени
  product-a.tokens.json # Перевизначення для Product A
  product-b.tokens.json # Перевизначення для Product B
```

Правила Theme Contract:
- Базові токени не змінюються між продуктами
- Перевизначення тільки через семантичні токени
- Кожен продукт має свій `theme` provider
- Компоненти не знають про конкретний продукт

Переваги:
- Єдина кодова база компонентів
- Консистентний UI
- Швидка кастомізація під бренд

