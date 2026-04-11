# Conventions

## Naming

| Construct | Style | Example |
|-----------|-------|---------|
| React components | PascalCase | `UserProfile.tsx` |
| Functions & hooks | camelCase | `formatDate()`, `useAuth()` |
| Constants | SCREAMING_SNAKE_CASE | `MAX_RETRIES = 3` |
| Types & interfaces | PascalCase | `type UserRole = ...` |
| Filenames | kebab-case | `user-profile.tsx` |
| CSS / Tailwind | utility classes only — avoid custom class names unless unavoidable | |

## Imports

Always in this order, separated by blank lines:

```typescript
// 1. External packages
import { useState } from 'react';
import { z } from 'zod';

// 2. Internal aliases
import { db } from '@/lib/db';
import type { User } from '@/types/user';

// 3. Relative imports
import { formatDate } from './utils';
```

## Code Style

- `const` over `let`; never `var`
- Named exports over default exports (easier to grep and refactor)
- `type` over `interface` unless you need declaration merging
- No `any` — use `unknown` + type narrowing, or define a proper type
- Co-locate styles, tests, and types with the component they belong to
- Prefer `async/await` over `.then()` chains

## Commit Messages

Format: `type(scope): short description` — imperative mood, lowercase, no trailing period, under 72 characters.

Types: `feat` · `fix` · `refactor` · `test` · `docs` · `chore` · `perf` · `ci`

```
feat(auth): add Google OAuth provider
fix(api): handle expired tokens in refresh flow
test(utils): add edge cases for formatDate
chore(deps): upgrade prisma to v5
```

## PR and Issue Comment Formatting

Write each paragraph as a **single continuous line** with no embedded newlines. GitHub renders bare newlines as line breaks, causing mid-sentence breaks in the rendered output. Separate paragraphs with a blank line.

**Correct**:
```
This PR adds Google OAuth as an authentication provider alongside the existing email/password login.

The NextAuth.js Prisma adapter stores provider tokens so downstream API calls can use them without re-authentication.
```

**Incorrect** (hard-wrapped):
```
This PR adds Google OAuth as an authentication provider
alongside the existing email/password login.
```

PR titles: `type(scope): description` — under 70 characters. Use the body for detail.
