# TAURI_ARCHITECTURE_STANDARD

## Desktop Application Stack

**Frontend**: React + TypeScript — тільки UI
**Backend**: Rust
**Shell**: Tauri

Архітектура чітко розділена. Немає прямого доступу до системи з фронтенду.

## Architecture Flow

```
Frontend UI (React)
    ↓ Tauri Commands / IPC
Rust Backend
    ↓ Native APIs
Operating System
```

## Principles

- **Frontend only UI.** Ніякої бізнес-логіки в React, ніякого доступу до файлів/процесів.
- **Rust owns privileged operations.** Всі небезпечні операції виконує Rust.
- **IPC is the boundary.** Tauri Commands — єдиний місток між frontend і backend.
- **Security by default.** Мінімально необхідні permissions.

## IPC

### Tauri Commands
- Всі комунікації через `invoke()` / `command`
- Команди оголошуються в `src-tauri/src/main.rs`
- Frontend викликає команду через `window.__TAURI__.core.invoke()`

Приклад:
```rust
#[tauri::command]
fn read_file(path: String) -> Result<String, String>
```

```ts
const content = await invoke<string>('read_file', { path })
```

### Rules
- Кожна команда має опис і документацію
- Тасувати параметри через strongly typed DTO
- Обробка помилок через `Result<T, E>`
- Немає можливості викликати Rust напряму без команди

## Permissions

### Tauri Capabilities
- Всі permissions оголошуються в `tauri.conf.json`
- Мінімальні права на кожен команд
- Ніяких wildcard permissions

### Access Control
- Читання файлів — тільки в дозволених директоріях
- Запис файлів — тільки в app data folder
- Network — тільки потрібні хости
- System commands — заборонені за замовчуванням

## Security

- **Frontend не має прямого доступу до filesystem.** Тільки через команди
- **Rust валідує всі вхідні дані.** Ніякої довіри до фронтенду
- **Content Security Policy строгий.** No `unsafe-inline`, no `eval`
- **Commands whitelist.** Тільки оголошені команди доступні фронтенду
- **Sanitize paths.** Перевірка на path traversal attacks
- **No secrets in frontend.** Всі токени/ключі в Rust

## Storage

- **Local storage**: LocalStorage для UI стану
- **Secure storage**: Tauri Store / Keychain через Rust команди
- **File storage**: App data directory через Rust
- **Database**: SQLite via Rust, доступ через команди

Заборонено:
- `localStorage` для чутливих даних
- Direct file access з фронтенду

## Native Integrations

Через Rust backend:

- **Filesystem** — читання/запис файлів
- **System notifications** — `tauri-plugin-notification`
- **Tray icon** — `tauri-plugin-tray`
- **Auto-updater** — `tauri-plugin-updater`
- **Deep links** — `tauri-plugin-deep-link`
- **Native dialogs** — `tauri-plugin-dialog`

Frontend викликає через команди, не напряму.

## Rules

- Frontend не має прямого доступу до filesystem. Тільки через Tauri Commands.
- Rust відповідає за privileged operations: файли, процеси, мережа, system API.
- Всі команди мають ID, опис, валідацію параметрів.
- UI компоненти не знають про Rust реалізацію.
- Помилки передаються як structured JSON, не raw strings.
- Не можна винести бізнес-логіку в фронтенд.
- Кожна команда має тести на обидві сторони IPC.

## Project Structure

```
src/
  app/
  components/
  features/
  services/              # Tauri commands wrapper
    tauri.ts
  types/
src-tauri/
  src/
    main.rs             # Commands definition
    lib.rs
  Cargo.toml
```

**services/tauri.ts** — єдиний фасад для всіх Tauri команд.

## Forbidden Patterns

- Direct filesystem access from React
- Synchronous IPC calls
- Sending secrets via invoke
- Rust код без валідації вхідних даних
- Чутливі дані в LocalStorage
- Commands без type safety
