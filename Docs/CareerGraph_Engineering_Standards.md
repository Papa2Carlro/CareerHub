# CareerGraph Engineering Standards

**Status:** Standards defined from documentation canon
**Date:** 2026-08-19
**Note:** These standards are based on documented intentions, not enforced code

## 1. Project Setup Requirements

### Technology Stack (Planned)

**Frontend:**
- Framework: React + TypeScript
- UI: Tailwind CSS or SCSS Modules
- State: Zustand (view-scoped) + React Query/SWR for server state
- Build: Vite
- Package manager: npm or pnpm

**Backend:**
- Framework: Tauri + Rust
- Database: SQLite
- Domain SoT: Python worker via MCP

**Non-negotiable:**
- Local-first - must work offline
- No cloud dependencies for core features
- SQLite as source of truth

### Repository Structure

```
CareerHub/
├── apps/
│   ├── web/                 # Tauri frontend
│   └── desktop/             # Tauri app wrapper
├── packages/
│   ├── shared/              # Shared types
│   ├── ui/                  # Shared components
│   └── domain/              # Business logic
├── docs/                    # Documentation
└── scripts/                 # Build scripts
```

**Current reality:** Structure not implemented

---

## 2. Frontend Standards

### File Organization

**Component rule:** One folder = one component
```
components/Profile/Skills/
  Skills.tsx              # Named export
  Skills.module.scss      # Styles
  Skills.types.ts         # Types
  index.ts               # Re-export
  __tests__/
    Skills.test.tsx
```

**Page rule:** Pages in `pages/` or `app/` directory
```
pages/
  Profile/
    ProfilePage.tsx
    ProfilePage.module.scss
```

**Feature organization:**
```
features/
  profile/
    components/
    hooks/
    services/
    types/
  vacancies/
    components/
    hooks/
    services/
    types/
```

### Naming Conventions

**Files:**
- Components: PascalCase `Skills.tsx`
- Hooks: camelCase `useProfile.ts`
- Types: PascalCase `ProfileType.ts`
- Utilities: camelCase `formatDate.ts`
- SCSS modules: `ComponentName.module.scss`
- SCSS partials: `_name.scss`

**Variables:**
- const: camelCase
- Types/Interfaces: PascalCase
- Enums: PascalCase
- CSS classes: PascalCase root, BEM elements

### TypeScript Rules

**Strict mode:** Enabled
```json
{
  "strict": true,
  "noImplicitAny": true,
  "strictNullChecks": true
}
```

**Component pattern:**
```tsx
import { FC } from 'react';
import { ProfileProps } from './Profile.types';
import styles from './Profile.module.scss';

export const Profile: FC<ProfileProps> = ({ name, skills }) => {
  return <div className={styles.Profile}>{name}</div>;
};
```

**Never:**
- `any` type
- Default exports for components
- Prop drilling without context/hooks
- Business logic in components

### Styling Standards

**SCSS Modules + BEM:**

```scss
// Profile.module.scss
.Profile {
  display: flex;
  
  &__header {
    font-size: 1.5rem;
  }
  
  &__content {
    padding: 1rem;
  }
  
  &.active {
    background: blue;
  }
  
  &--large {
    font-size: 2rem;
  }
}
```

**classnames/bind usage:**
```tsx
import classNames from 'classnames/bind';
import styles from './Profile.module.scss';

const cn = classNames.bind(styles);

export const Profile = () => {
  return <div className={cn('Profile', { active: isActive })} />;
};
```

**Variables:**
- Use CSS custom properties for theme
- SCSS variables in abstracts
- No hardcoded colors

### Imports Ordering

1. React / external libraries
2. Internal packages
3. Relative imports
4. Styles

```tsx
import { useState } from 'react';
import { Button } from '@ui/Button';
import { useProfile } from '@/features/profile/hooks';
import styles from './Profile.module.scss';
```

### Hooks Rules

**Custom hooks:**
- Name starts with `use`
- File: `useSomething.ts`
- Only call hooks at top level
- Return memoized values

```ts
export const useProfile = (id: string) => {
  const [profile, setProfile] = useState<Profile | null>(null);
  
  // Logic
  
  return useMemo(() => ({ profile, loading }), [profile]);
};
```

**Domain hooks vs UI hooks:**
- Domain hooks: data fetching, business logic
- UI hooks: view state, form state
- Never mix

### State Management

**Zustand view-scoped:**
```ts
// stores/profileStore.ts
export const createProfileStore = () => createStore<ProfileState>()(
  (set) => ({
    viewState: 'idle',
    setViewState: (state) => set({ viewState: state })
  })
);
```

**Rules:**
- View state only in Zustand
- Domain state in React Query
- No duplication
- Factory pattern for view stores

### Form Handling

**Use React Hook Form:**
```tsx
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';

const schema = z.object({ name: z.string() });

export const ProfileForm = () => {
  const { register, handleSubmit } = useForm({
    resolver: zodResolver(schema)
  });
  
  return <form onSubmit={handleSubmit(onSubmit)}>{/* ... */}</form>;
};
```

**Validation:**
- Zod schemas
- Client + server validation
- Error messages user-friendly

### Error Handling

**Component error boundaries:**
```tsx
class ErrorBoundary extends Component {
  componentDidCatch(error, info) {
    // Log error
  }
}
```

**Async errors:**
```ts
try {
  await fetchData();
} catch (error) {
  // Log, show user-friendly message
  // Never silent fail
}
```

---

## 3. Backend Standards

### Rust Tauri Standards

**Module structure:**
```
src-tauri/src/
├── commands/          # Tauri commands
├── domain/           # Business logic
├── db/               # Database layer
├── models/           # Types
└── lib.rs           # Entry point
```

**Command pattern:**
```rust
#[tauri::command]
pub async fn create_profile(profile: Profile) -> Result<Profile, String> {
    // Validation
    // Business logic
    // Return result
}
```

**Error handling:**
- Use `Result<T, String>`
- Never panic
- Log errors properly

### Database Standards

**SQLite best practices:**
```sql
PRAGMA foreign_keys = ON;
PRAGMA journal_mode = WAL;
PRAGMA busy_timeout = 30000;
```

**Migration naming:**
` migrations/001_create_profiles.sql`

**Table naming:**
- snake_case
- Plural: `profiles`, `skills`, `vacancies`

**Indexes:**
- Index all foreign keys
- Index frequently queried columns
- Composite indexes for queries

### API Layer

**Request/Response types:**
```rust
#[derive(Serialize, Deserialize)]
pub struct CreateProfileRequest {
    pub name: String,
    pub email: String,
}

#[derive(Serialize)]
pub struct CreateProfileResponse {
    pub id: String,
    pub name: String,
}
```

**Validation:**
- Validate at command boundary
- Use serde for deserialization
- Return meaningful errors

---

## 4. Code Quality

### Formatting

**Prettier config:**
```json
{
  "semi": true,
  "tabWidth": 2,
  "useTabs": false,
  "singleQuote": false,
  "trailingComma": "es5",
  "printWidth": 120
}
```

### Linting

**ESLint:**
- React recommended
- TypeScript recommended
- Import ordering
- No unused vars

**Rust:**
- clippy enforced
- fmt enforced

### Git

**Commit messages:**
```
type(scope): description

feat(profile): add skills management
fix(vacancy): handle import errors
docs(readme): update installation
```

**Branch naming:**
- `feature/profile-skills`
- `fix/vacancy-import`
- `docs/architecture`

---

## 5. Development Workflow

### Local Development

**Setup:**
```bash
# Frontend
pnpm install
pnpm dev

# Backend
cargo run

# Database
# SQLite file created automatically
```

**Environment variables:**
```env
# .env.local
DATABASE_PATH=./data/careergraph.db
LOG_LEVEL=debug
```

### Testing

**Unit tests:**
- Jest for frontend
- cargo test for backend
- Coverage > 80%

**Integration tests:**
- Test API endpoints
- Test database operations
- Test critical paths

**E2E tests:**
- Playwright for UI
- Test happy paths

### Build & Release

**Build:**
```bash
pnpm build
cargo build --release
```

**Release checklist:**
- Tests pass
- Lint passes
- Type check passes
- Changelog updated
- Version bumped

---

## 6. Feature Creation Contract

### How to create a feature

1. **Documentation first**
   - Create ADR if architectural decision
   - Update product docs
   - Define domain model

2. **Types first**
   - Define TypeScript types
   - Define Rust structs
   - Database schema

3. **Backend first**
   - Implement domain logic
   - Add validation
   - Add tests

4. **Frontend second**
   - Create components
   - Add hooks
   - Add tests

5. **Integration**
   - Connect frontend to backend
   - E2E tests
   - Documentation

### Where business logic lives

**Never in components.**
**Never in UI hooks.**

Business logic:
- Rust domain layer
- Python domain SoT
- Shared packages/domain

UI logic:
- React hooks
- Zustand stores
- Component state

### Forbidden patterns

❌ Business logic in components
❌ API calls in components (use hooks)
❌ Direct database access from UI
❌ Any type
❌ Prop drilling > 2 levels
❌ God components
❌ Magic numbers
❌ Console.log in production
❌ Unvalidated user input

### Required patterns

✅ Separation of concerns
✅ Type safety
✅ Error boundaries
✅ Loading states
✅ Empty states
✅ Optimistic updates
✅ Debounced inputs
✅ Memoized computations
✅ Clean architecture

---

## 7. Dangerous Areas

### Critical rules

1. **Database migrations**
   - Never modify existing migrations
   - Always test rollback
   - Backup before migrate

2. **Domain logic**
   - Changes affect all features
   - Requires full test suite
   - Code review mandatory

3. **State management**
   - Global state changes are risky
   - Test thoroughly
   - Document changes

4. **API contracts**
   - Breaking changes need versioning
   - Deprecate gradually
   - Document all changes

---

## 8. Engineering Principles

### Core principles

1. **Truth over beauty**
   - Data integrity > UI polish
   - Accurate > Pretty

2. **Local-first**
   - Works offline
   - User owns data
   - Sync optional

3. **Structured data**
   - Domain model first
   - Types everywhere
   - Validation always

4. **Evidence-based**
   - Every skill needs evidence
   - Every decision needs reason
   - Every change needs test

5. **Fail safe**
   - Validate input
   - Handle errors gracefully
   - Never lose user data

---

## 9. Onboarding Checklist

New engineer should:

- [ ] Read product documentation
- [ ] Read architecture docs
- [ ] Set up local environment
- [ ] Run tests
- [ ] Make small fix
- [ ] Understand domain model
- [ ] Know where business logic lives
- [ ] Know error handling patterns
- [ ] Know state management
- [ ] Review code standards

Time to productivity: < 1 day

---

## 10. Compliance

These standards are **mandatory** for all code.

**Review checklist:**
- [ ] Follows naming conventions
- [ ] Types defined
- [ ] Tests added
- [ ] Lint passes
- [ ] Format correct
- [ ] Documentation updated
- [ ] No business logic in UI
- [ ] Error handling present
- [ ] Loading states handled

**Violation consequences:**
- Code review rejection
- Merge blocked
- Technical debt logged

---

## Appendix: Migration from Current State

**Current state:** No code exists

**Required setup:**
1. Initialize Tauri project
2. Set up React + TypeScript
3. Configure Prettier/ESLint
4. Set up SQLite with WAL mode
5. Create initial schema
6. Implement domain model
7. Add first feature (Profile Manager)

**Timeline estimate:** 2-3 weeks for MVP scaffold

---

*Last updated: 2026-08-19*
*Status: Standards defined, not enforced*
*Next: Implement scaffolding*
