# DATABASE_STANDARD

## PostgreSQL Default

### Migrations
- **Tool**: `prisma migrate` / `typeorm migration`
- **Naming**: `YYYYMMDDHHMMSS_description`
- **Never** commit raw SQL changes without migration
- **Branch-aware**: separate branches per feature
- **Always** reversible migrations (up/down)

### Indexes
- **Named indexes**: `idx_table_column` format
- **Never** без іменованих індексів — вони потрібні для downgrade
- **Only** індекси, які критичні для query performance
- **Partial indexes** для фільтрацій з філтром `WHERE`
- **Covering indexes** для багатьох полів
- Index definitions зберігаються у migrations

### Transactions
- **Every** write operation через `beginTransaction` / `commit` / `rollback`
- **Never** auto-commit для DELETE/UPDATE/INSERT
- **Idempotent** retry логика для distributed systems
- NestJS/Prisma `transaction()` decorator
- Savepoints дещо потрібно

### ORM Rules
- **TypeORM / Prisma** обов'язково, нікуди raw SQL
- Entities типізовані, мають explicit relationships
- Lazy loading вимкнути, використовувати `eager` там де потрібно
- **Never** n+1 проблема — явно заводити `relations`
- Value Objects не зберігаються в БД самостійно
- Soft delete як замовчування, можна вимкнути

### Schema Ownership
- **Tables 소유**: `public`.`table` ніколи без схеми
- **Roles**: `application` user має тільки `SELECT/INSERT/UPDATE/DELETE`
- **Superuser**: тільки у development
- **Schema separation** для multi-tenant: `tenant_id` в кожній таблиці
- **Migration owner**: чіткий відповідальник

### Forbidden Patterns
- Бізнес логіка в контролерах (репетиція)
- Ручні `ALTER TABLE` production без migration
- `SELECT *` у production запитах
- Missing indexes на колонах у WHERE/ORDER BY/JOIN
- N+1 queries без надзвичайної причини
- Hardcoded connection strings
- Missing foreign key constraints
- Truncate tables production без п integrals
- ORM конфігурація без типів

## Engineering Standard

Цей стандарт обов'язковий для всіх баз даних, незалежно від мови.
Database consistency важливіша швидкості розробки.
