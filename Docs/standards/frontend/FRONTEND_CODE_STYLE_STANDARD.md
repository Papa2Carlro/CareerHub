# FRONTEND_CODE_STYLE_STANDARD

## TypeScript Rules

### Naming Conventions
- **Files**: `kebab-case.ts` для утиліт, `ComponentName.tsx` для компонентів
- **Components**: `PascalCase`
- **Functions/Variables**: `camelCase`
- **Constants**: `UPPER_SNAKE_CASE`
- **Types/Interfaces**: `PascalCase`
- **Enums**: `PascalCase`

### Types vs Interfaces
- Використовувати `type` для union types, intersection, mapped types
- Використовувати `interface` для об'єктів які будуть розширюватись іншими `interface`
- Для публічних API перевага `interface`
- Ніколи не мішати без причини

### Enums Policy
- Заборонено числові enums. Тільки string enums
- Для конечних наборів значень використовувати `as const` + `typeof`
- Enum мають бути в `shared/` або в `features/*/types/`

### Readonly Usage
- Всі пропси компонентів `readonly`
- Всі типи даних з сервера `Readonly` або `readonly` поля
- Ніколи не мутувати аргументи функцій
- Використовувати `ReadonlyArray<T>` для іммутабельних списків

### Error Handling
- Обов'язкова типізація помилок: `Error | CustomError`
- Ніколи не ловити `unknown` без перевірки типу
- Використовувати `Result<T, E>` патерн для бізнес-логіки
- Логи помилок через централізований error boundary + reporter

## React Rules

### Component Rules
- Функціональні компоненти тільки
- Компонент в одному файлі, одна відповідальність
- Максимум 200 рядків, інакше розбивати
- Компонент експортується як `export default` через `index.ts`

### Props Design
- Пропси типізуються окремим `ComponentName.types.ts`
- Пропси розбиваються на required/optional
- Ніколи не використовувати `any` в пропсах
- Default values через default parameters, не через `defaultProps`

### Hooks Rules
- Custom hooks мають префікс `use`
- Хуки живуть в `features/*/hooks/`
- Ніколи не викликати хуки умовно
- Хуки не мають side effects в тілі, тільки в `useEffect`
- Dependency array завжди повний та коректний

### Composition Pattern
- Композиція > перевизначення пропсів
- Compound components для складних UI
- Render props тільки як останній засіб
- Не створювати God components

## File Structure

```
ComponentName/
  ComponentName.tsx
  ComponentName.module.scss
  ComponentName.types.ts
  index.ts
```

- `ComponentName.tsx` — логіка компонента
- `ComponentName.module.scss` — стилі тільки для компонента
- `ComponentName.types.ts` — типи пропсів і внутрішні типи
- `index.ts` — barrel export

## CSS Standards

### Design Tokens
- Всі кольори, spacing, typography — тільки через токени
- Токени зберігаються в `styles/tokens/`
- Ніяких хардкод значень в компонентах

### BEM + SCSS Modules
- SCSS Modules обов'язково
- БЕМ-методологія всередині модуля: `.block__element--modifier`
- Глобальні стилі тільки в `styles/`

### No Random Values
- Заборонено магічні числа
- Заборонено `px` в коді, тільки токени
- Використовувати `rem`/`em` через токени

## Imports Order

1. external
2. internal absolute
3. relative

```ts
import React from 'react';
import { useQuery } from '@tanstack/react-query';
import { Button } from '@components/Button';
import { formatDate } from '@/shared/utils/date';
import { styles } from './ComponentName.module.scss';
import { useLocalHook } from './useLocalHook';
```

- Абсолютні імпорти через `@/` або `@components/`
- Ніколи не імпортувати з `../..` більше ніж на 2 рівні

## Заборонені практики

- `any` без пояснення в коментарі `// eslint-disable-next-line @typescript-eslint/no-explicit-any -- reason`
- Business logic в JSX. Логіка тільки в hooks/services
- Дублювання компонентів. Перевірити `components/` перед створенням
- Мутація пропсів
- Inline anonymous functions в render списків
- `console.log` в production коді
- Магічні числа і строки
- Змішування TypeScript стилів в одному файлі

## Engineering Standard

Цей стандарт обов'язковий для всього фронтенду. Code review блокується при порушеннях. Стабільність архітектури важливіша ніж швидкість написання коду.
