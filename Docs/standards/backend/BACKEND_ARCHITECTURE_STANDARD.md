# BACKEND_ARCHITECTURE_STANDARD

## Stack

Default: Node.js + TypeScript + NestJS
Compatible: Python FastAPI, Go

Стандарт застосовується для всіх backend сервісів незалежно від мови.

## Архітектура: Modular Clean Architecture

Чиста архітектура з чіткими межами шарів. Залежності спрямовані всередину.

### Flow

```
Controller
    ↓
Service
    ↓
Domain
    ↓
Repository
    ↓
Database
```

Кожен шар знає тільки про шар всередині. Зовнішні деталі ізольовані.

## Project Structure

```
src/
  modules/           # Бізнес-модулі
    [module-name]/
      controller/
      service/
      domain/
      repository/
      dto/
      entities/
      index.ts
  common/            # Shared primitives
    decorators/
    pipes/
    guards/
    interceptors/
    filters/
    types/
  config/            # Конфігурація середовища
  database/          # Міграції, seeds, коннекти
  security/          # Auth, authorization, encryption
  logger/            # Логування, correlation id
```

## Шари

### Controller
- Тонкий шар. Тільки HTTP/transport
- Валідація DTO через pipes
- Виклик сервісу, повернення відповіді
- Без бізнес-логіки, без доступу до БД
- nestjs: `@Controller()`, `@Get()`, `@Post()`

### Service
- Оркестрація бізнес-процесів
- Виклик domain logic
- Транзакційність
- Не знає про HTTP, знає про domain

### Domain
- Чиста бізнес-логіка, без зовнішніх залежностей
- Entities, Value Objects, Domain Services
- Не залежить від інфраструктури
- Тестується без моків БД

### Repository
- Абстракція над даними
- Реалізація в `infrastructure/`
- Інтерфейс в `domain/`
- Повертає domain entities, не raw DB records

### DTO
- Data Transfer Objects для входу/виходу
- Валідація через class-validator
- Сильно типізовані
- Відділені від entities

### Entities
- Domain entities
- Валідація інваріантів
- Методи доменної логіки
- Не містять персистентні деталі

## Modularity

Кожен модуль ізольований:

- Власний контролер, сервіс, репозиторій
- Публічний API через `index.ts`
- Внутрішні деталі приватні
- Модулі не знають про один одного без явної залежності
- Shared код тільки в `common/`

## Rules

- **Controller thin.** Максимум 10 рядків на обробник. Логіка в сервіс.
- **Business logic in services/domain.** Ніякої логіки в контролері чи репозиторії.
- **Database isolated.** Доступ до БД тільки через Repository. Жодних SQL в сервісах.
- **DTO != Entity.** Ніколи не повертати entity напряму в HTTP.
- **Dependency Inversion.** Модулі залежать від абстракцій, не від реалізацій.
- **NestJS Modules.** Кожен модуль реєструється в `Modules` з чіткими `imports/exports`.
- **Async everywhere.** Асинхронні операції завжди через `async/await`.

## Forbidden Patterns

- Бізнес-логіка в контролері
- Прямі SQL запити в сервісах
- Return raw DB models в API
- Мішанина валідації в контролері і сервісі
- Спіральні імпорти між модулями
- Глобальний стан в сервісах
- Змішування DTO і entities
- Відсутність транзакцій при багатокрокових операціях
- Хардкод конфігурації в коді
- Логування без correlation id

## Cross-Language Compatibility

Для Python FastAPI і Go той самий принцип шарів:

- Controller → Service → Domain → Repository → DB
- Структура проєкту адаптована під мову
- Інтерфейси репозиторіїв аналогічні
- Чиста архітектура зберігається
