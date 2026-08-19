# UI Design System Standard

**Status:** Universal engineering contract
**Date:** 2026-08-19
**Scope:** Project-independent UI system protocol

## 1. Philosophy

**Core principles:**

- **Consistency over speed** - Reuse before creating new
- **Components over duplication** - One source of truth per UI pattern
- **Tokens over hardcoded values** - Never hardcode colors, spacing, typography
- **Semantic naming over visual naming** - Name by purpose, not appearance
- **Accessibility by default** - All components must be accessible
- **Migration-friendly architecture** - Easy to refactor, hard to break

**Problem this solves:**
Every project starts from zero and accumulates its own UI dialect within a month.

Project A: `screen-card`, `btn-primary`, `text-muted`
Project B: `panel`, `action-button`, `secondary-text`

Functionally identical, semantically different.

This standard prevents UI dialect fragmentation.

---

## 2. Design Tokens

Design tokens are the source of truth for all visual values.

Components never use concrete values. Only semantic tokens.

### Colors

**Required semantic categories:**

- `background` - Page background
- `surface` - Card, panel background
- `surface-elevated` - Modal, dropdown background
- `overlay` - Modal backdrop
- `text-primary` - Primary text
- `text-secondary` - Secondary text
- `text-muted` - Disabled/muted text
- `text-disabled` - Disabled text
- `border` - Default borders
- `border-subtle` - Subtle borders
- `accent` - Primary accent
- `success` - Success states
- `warning` - Warning states
- `danger` - Error/danger states
- `info` - Information states

**Rule:**
BAD:
```scss
color: #888;
background: #121212;
```

GOOD:
```scss
color: var(--text-muted);
background: var(--surface);
```

**Forbidden:**
- Hex codes in components
- RGB values in components
- Hardcoded colors anywhere except tokens file

### Typography

**Required tokens:**

- Font families:
  - `font-sans` - Primary sans-serif
  - `font-mono` - Monospace
  - `font-display` - Display/heading

- Font sizes:
  - `text-xs` - 12px
  - `text-sm` - 14px
  - `text-base` - 16px
  - `text-lg` - 18px
  - `text-xl` - 20px
  - `text-2xl` - 24px
  - `text-3xl` - 30px
  - `text-4xl` - 36px

- Font weights:
  - `font-normal` - 400
  - `font-medium` - 500
  - `font-semibold` - 600
  - `font-bold` - 700

- Line heights:
  - `leading-tight` - 1.25
  - `leading-normal` - 1.5
  - `leading-relaxed` - 1.75

**Usage:**
```scss
font-family: var(--font-sans);
font-size: var(--text-base);
font-weight: var(--font-medium);
line-height: var(--leading-normal);
```

### Spacing

**Single scale for all spacing:**

- `space-xs` - 4px
- `space-sm` - 8px
- `space-md` - 16px
- `space-lg` - 24px
- `space-xl` - 32px
- `space-2xl` - 48px
- `space-3xl` - 64px

**Usage:**
```scss
padding: var(--space-md) var(--space-lg);
margin-bottom: var(--space-sm);
gap: var(--space-md);
```

**Forbidden:**
- Random pixel values
- Magic numbers
- Inconsistent spacing

### Radius

**Standardized:**

- `radius-sm` - 4px - Small controls
- `radius-md` - 8px - Cards, inputs
- `radius-lg` - 12px - Modals, large surfaces
- `radius-full` - 999px - Pills, badges

### Shadows

**Elevations:**
- `shadow-sm` - Subtle
- `shadow-md` - Card
- `shadow-lg` - Modal
- `shadow-xl` - Dropdown

### Animation

**Timing:**
- `duration-fast` - 150ms
- `duration-normal` - 250ms
- `duration-slow` - 350ms

**Easing:**
- `ease-in-out` - Default
- `ease-out` - Entrance
- `ease-in` - Exit

---

## 3. Component Architecture

### Folder Structure

**Standard:**
```
components/ui/Button/

Button.tsx
Button.module.scss
Button.types.ts
index.ts
```

**Rules:**
- One component = one folder
- Named exports only
- Component owns styles
- No global component styles
- Types in separate file
- Tests in `__tests__/` subdirectory

### Naming

**Component names:**
- PascalCase: `Button`, `DataTable`
- Folder: PascalCase

**File names:**
- Component: `Button.tsx`
- Styles: `Button.module.scss`
- Types: `Button.types.ts`
- Test: `Button.test.tsx`

**CSS classes:**
- Root: `ComponentName`
- BEM elements: `ComponentName__element`
- BEM modifiers: `ComponentName--modifier`
- State: `ComponentName.is-active`

---

## 4. Styling Rules

### CSS Modules / SCSS Modules

**Required:**
- All components use CSS Modules
- No global CSS for components
- No inline styles without reason

**BEM naming:**
```scss
.Button {
  padding: var(--space-sm) var(--space-md);
  border-radius: var(--radius-md);
  font-size: var(--text-base);
  
  &__icon {
    margin-right: var(--space-sm);
  }
  
  &--primary {
    background: var(--accent);
    color: var(--text-on-accent);
  }
  
  &--secondary {
    background: var(--surface);
    color: var(--text-primary);
  }
  
  &.disabled {
    opacity: 0.5;
    pointer-events: none;
  }
  
  &:hover:not(.disabled) {
    opacity: 0.9;
  }
  
  &:focus-visible {
    outline: 2px solid var(--accent);
    outline-offset: 2px;
  }
}
```

### classnames/bind

**Required for conditional classes:**
```tsx
import classNames from 'classnames/bind';
import styles from './Button.module.scss';

const cn = classNames.bind(styles);

export const Button = ({ variant, disabled, ...props }) => {
  return (
    <button
      className={cn('Button', {
        'Button--primary': variant === 'primary',
        disabled
      })}
      disabled={disabled}
      {...props}
    />
  );
};
```

**Forbidden:**
- Template literals for classes
- Array joins for classes
- Inline style objects for layout

### Specificity

**Max specificity: 0,1,0**
- No IDs
- No `!important`
- No deep nesting (> 3 levels)

---

## 5. Component Categories

### Atoms

**Basic building blocks:**

- Button
- Input
- TextArea
- Select
- Checkbox
- Radio
- Switch
- Badge
- Icon
- Spinner
- Avatar
- Tag

**Characteristics:**
- No business logic
- Fully controlled
- Configurable via props
- Accessible by default

### Molecules

**Combinations of atoms:**

- FormField (Label + Input + Error)
- SearchInput (Input + Icon + Clear button)
- ButtonGroup
- Tabs
- Dropdown
- Pagination
- Breadcrumbs
- CardHeader
- Stat

**Characteristics:**
- Reusable across features
- Consistent API
- Minimal business logic

### Organisms

**Complex components:**

- DataTable
- Navigation
- DashboardCard
- Modal
- Drawer
- Sidebar
- Header
- Footer
- Form

**Characteristics:**
- Feature-specific but reusable
- Composed of molecules
- May contain business logic

**Rule:** Components must be composable, not monolithic.

---

## 6. Required Core Components

### Controls

**Must exist:**
- Button (variants: primary, secondary, ghost, danger)
- Input (with error, disabled states)
- TextArea
- Select (native and custom)
- Checkbox
- Radio
- Switch

### Feedback

**Must exist:**
- Toast
- Alert
- EmptyState
- LoadingState
- ErrorState
- Skeleton

### Navigation

**Must exist:**
- Tabs
- Breadcrumbs
- Pagination
- Sidebar
- Header

### Layout

**Must exist:**
- Card
- Stack (flex)
- Container
- Divider
- Grid
- Modal

### Data Display

**Must exist:**
- DataTable
- List
- Badge
- Tag
- Avatar
- Progress

---

## 7. Component API Rules

### Props Standard

**Every component must support:**

- `variant` - Visual style variant
- `size` - Size variant
- `disabled` - Disabled state
- `loading` - Loading state
- `className` - Custom class override
- `style` - Inline style override (sparingly)

**Example:**
```tsx
<Button
  variant="primary"
  size="small"
  loading
  disabled
  onClick={handleClick}
/>
```

**Forbidden:**
```tsx
<Button blue small rounded />
```

**Bad:**
```tsx
<Button color="#ff0000" fontSize="12px" />
```

**Good:**
```tsx
<Button variant="danger" size="sm" />
```

### State Variants

**Every component must handle:**
- Default
- Hover
- Focus
- Active
- Disabled
- Loading
- Error

**Every component must be:**
- Keyboard accessible
- Screen reader friendly
- Color contrast compliant
- Focus visible

### Accessibility Minimum

- Semantic HTML
- ARIA labels where needed
- Keyboard navigation
- Focus management
- Color contrast 4.5:1 minimum
- No color-only information

---

## 8. Migration Strategy

### Phase 1: Tokens
1. Define design tokens
2. Create tokens file
3. Document token usage
4. No components yet

**Output:** `tokens.css` or `tokens.scss`

### Phase 2: Atomic Components
1. Build atoms
2. Test in isolation
3. Document API
4. No integration yet

**Output:** `components/ui/*` with atoms

### Phase 3: Replace Duplicated Patterns
1. Identify duplicated UI patterns
2. Create molecules
3. Replace duplicates
4. Measure coverage

**Output:** Reduced duplication

### Phase 4: Remove Old Styles
1. Audit legacy styles
2. Remove unused CSS
3. Delete old components
4. Update all references

**Output:** Clean codebase

### Migration Principles

- Never change both API and style simultaneously
- Maintain backward compatibility during migration
- Document breaking changes
- Test visual regression
- Rollback plan ready

---

## 9. UI Review Checklist

**Before merge, component must:**

- [ ] Use design tokens for all values
- [ ] No hardcoded colors/spacing/typography
- [ ] No duplication of existing patterns
- [ ] Component is reusable
- [ ] Has loading state
- [ ] Has error state
- [ ] Has empty state (if applicable)
- [ ] Accessible (keyboard, screen reader)
- [ ] Responsive
- [ ] Tests exist
- [ ] Storybook/docs exist
- [ ] Follows naming conventions
- [ ] Follows folder structure
- [ ] No business logic in UI component

**Code review questions:**
1. Can this be composed from existing components?
2. Are tokens used correctly?
3. Is API consistent with similar components?
4. Are all states handled?
5. Is it accessible?

---

## 10. Framework Independence

### Design System is Framework-Agnostic

This standard works for:
- React
- Vue
- Svelte
- Solid
- Angular
- Tauri
- Electron
- Web Components

### Implementation Mapping

**React:**
```tsx
import styles from './Button.module.scss';
const cn = classNames.bind(styles);
```

**Vue:**
```vue
<style module>
/* Same BEM structure */
</style>
```

**Web Components:**
```css
:host { --tokens-used-here }
```

**Core principles remain:**
- Tokens first
- Components second
- BEM naming
- Semantic API
- Accessibility

### Portability

A component defined by this standard can be:
1. Reimplemented in any framework
2. Migrated between projects
3. Shared across products
4. Tested independently

**The contract is:** Tokens + Props API + CSS Modules + BEM

Not framework-specific implementation.

---

## 11. Source of Truth

This document is the single source of truth for UI system rules.

**Authority:**
- Design tokens
- Component API
- Naming conventions
- Styling rules
- Architecture principles

**Any new UI must conform.**

**Violations:**
- Code review rejection
- Merge blocked
- Technical debt logged

**Updates:**
- Changes require approval
- Breaking changes documented
- Migration guide provided
- Versioned

---

## 12. Anti-Patterns

### Forbidden

❌ **Visual naming:**
```scss
.red-button { }
.big-text { }
```

✅ **Semantic naming:**
```scss
.Button--danger { }
.text-display { }
```

❌ **Hardcoded values:**
```scss
color: #ff0000;
padding: 17px;
```

✅ **Tokens:**
```scss
color: var(--danger);
padding: var(--space-md);
```

❌ **Component duplication:**
```ts
// Project A
<ProjectCard />

// Project B  
<ProjectPanel />
```

✅ **Reusable component:**
```ts
<Card variant="project" />
```

❌ **Business logic in UI:**
```tsx
const Button = () => {
  const user = useAuth();
  if (!user) return null;
  return <button>...</button>;
};
```

✅ **Pure presentational:**
```tsx
const Button = ({ disabled, children }) => {
  return <button disabled={disabled}>{children}</button>;
};
```

---

## 13. Quick Start

### New Component Checklist

1. Create folder `components/ui/ComponentName/`
2. Create `ComponentName.tsx`
3. Create `ComponentName.module.scss`
4. Create `ComponentName.types.ts`
5. Use tokens for all values
6. Follow BEM naming
7. Add variants via props
8. Handle all states
9. Add accessibility
10. Export from `index.ts`

### Example Implementation

```
components/ui/Button/
  Button.tsx
  Button.module.scss
  Button.types.ts
  index.ts
  __tests__/
    Button.test.tsx
```

**Button.tsx:**
```tsx
import classNames from 'classnames/bind';
import styles from './Button.module.scss';
import { ButtonProps } from './Button.types';

const cn = classNames.bind(styles);

export const Button = ({ variant = 'primary', size = 'md', disabled, loading, children, ...props }: ButtonProps) => {
  return (
    <button
      className={cn('Button', `Button--${variant}`, `Button--${size}`, { disabled, loading })}
      disabled={disabled || loading}
      {...props}
    >
      {loading ? 'Loading...' : children}
    </button>
  );
};
```

**Button.module.scss:**
```scss
.Button {
  padding: var(--space-sm) var(--space-md);
  border-radius: var(--radius-md);
  font-family: var(--font-sans);
  font-size: var(--text-base);
  font-weight: var(--font-medium);
  cursor: pointer;
  transition: opacity var(--duration-fast) ease-in-out;
  
  &--primary {
    background: var(--accent);
    color: var(--text-on-accent);
  }
  
  &--secondary {
    background: var(--surface);
    color: var(--text-primary);
    border: 1px solid var(--border);
  }
  
  &.disabled {
    opacity: 0.5;
    pointer-events: none;
  }
}
```

---

## 14. Evolution

### Versioning

- Standard versioned independently
- Breaking changes bump major version
- New tokens additive only
- Components additive first, breaking later

### Feedback Loop

1. Components created
2. Patterns identified
3. Standard updated
4. Components refactored
5. Repeat

### Metrics

Track:
- Component reuse rate
- Token coverage
- Duplication percentage
- Migration progress
- Accessibility score

---

## Summary

This is a **UI Protocol**, not a UI Kit.

**The contract:**
- Design tokens as source of truth
- Semantic naming throughout
- Components as building blocks
- Accessibility by default
- Migration-friendly architecture

**Result:**
- Same functional UI across projects
- Different visual implementation optional
- Consistent developer experience
- Portable between frameworks
- Maintainable over time

**This standard enables:**
- DocHub → CareerGraph → Next Project
- Same rules, different products
- Code reuse
- Team velocity
- Quality consistency

---

*Standard version: 1.0*
*Last updated: 2026-08-19*
*Status: Active*
*Applies to all UI development*
