# Architecture

## File Structure

```
src/
  app/
    (auth)/        # route group: unauthenticated pages
    (app)/         # route group: authenticated pages
    api/           # API route handlers
  components/
    ui/            # primitive components (Button, Input, Modal, etc.)
    features/      # domain-specific components grouped by feature
  lib/             # third-party client configs — one file per service
  utils/           # pure helper functions — zero side effects, no lib/ imports
  hooks/           # React hooks — call utils or lib, not fetch directly
  types/           # TypeScript interfaces and enums — no runtime logic
  styles/          # global CSS only; component styles live next to components
```

## Key Patterns

**Data flow**: [e.g., External API → Server Component fetch → props to Client Components]

**Auth boundary**: [e.g., `src/middleware.ts` checks session on every request; pages assume user is authenticated and never re-check]

**State management**: [e.g., React Query for server/async state; local `useState` for ephemeral UI state; no global client store]

**DB access**: [e.g., All queries through `src/lib/db.ts` Prisma client — no raw SQL, no second Prisma instance]

**Error handling**: Throw domain errors at the service layer; catch and format only in API route handlers or top-level error boundaries. Never silently swallow errors.

**Environment variables**:
- `NEXT_PUBLIC_*` — safe to read in browser; expose intentionally
- All others — server-only; import only in server components, API routes, or `lib/`

## Do Not Touch Without Discussion

- `[PROTECTED_FILE_1]` — [reason it must not change]
- `[PROTECTED_FILE_2]` — [reason it must not change]
- `migrations/` — Never edit past migrations; always create a new one

## Dependency Rules

```
app/ → components/, hooks/, lib/, utils/, types/
components/ → hooks/, utils/, types/   (no lib/ imports in UI components)
hooks/ → lib/, utils/, types/
utils/ → types/                        (pure: no lib/, no hooks/)
lib/ → types/                          (no internal app/ imports)
```

Violations of these rules create circular dependencies. Flag them rather than working around them.
