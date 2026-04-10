# [PROJECT_NAME] — Agent Instructions

> Self-contained agent instructions for this repository. Compatible with any AI coding agent (Claude, Copilot, Cursor, Codex, Gemini, etc.).

## Project

[One to two sentences describing the project and its primary goal.]

**Stack**: [Framework] · [Language] · [Database] · [Auth] · [Styling]

## Commands

```bash
[INSTALL]       # install dependencies
[DEV]           # start dev server
[TEST_SINGLE]   # run one test by name: [INSTALL] -- -t "test name"
[TEST_ALL]      # run full test suite
[TYPECHECK]     # static type check (no emit)
[LINT]          # lint and auto-fix
[BUILD]         # production build
[MIGRATE]       # run database migrations
```

## Source Layout

```
src/
  app/          # routes & pages ([App Router / Pages Router])
  components/   # shared UI — presentational only
  lib/          # third-party clients — initialize once, import everywhere
  utils/        # pure helpers — no imports from lib/
  hooks/        # custom React hooks
  types/        # TypeScript definitions — no runtime logic
```

## Architecture

- **Data flow**: [e.g., API → Server Component → Client Component via props]
- **Auth boundary**: [e.g., Middleware-enforced; never trust client-supplied user IDs]
- **State**: [e.g., React Query for server state; Zustand for UI state]
- **DB access**: [e.g., Prisma ORM only — no raw SQL]
- **Error handling**: Throw at domain boundaries; catch only at API layer or error boundaries

**Do not touch**:
- `[e.g., src/lib/db.ts]` — DB singleton; editing breaks connection pooling
- `[e.g., src/middleware.ts]` — Auth enforcement; exceptions are intentional
- `[e.g., migrations/]` — Never edit past migrations; create new ones

## Conventions

**Naming**:
- `PascalCase` — components, types, interfaces
- `camelCase` — functions, variables, hooks
- `SCREAMING_SNAKE_CASE` — constants
- `kebab-case` — filenames

**Imports** (always in this order, blank line between groups):
1. External packages
2. Internal aliases (`@/...`)
3. Relative imports

**Commits**: `type(scope): short description` — imperative mood, no period.
Types: `feat` `fix` `refactor` `test` `docs` `chore` `perf` `ci`

**PRs and issue comments**: Write each paragraph as a single continuous line. No mid-sentence hard wraps — GitHub renders bare newlines as visible line breaks.

## Git Workflow

Branch naming: `type/short-description` (e.g., `feat/add-oauth`, `fix/token-refresh`)

1. Branch from `main` — never push directly to `main`
2. Implement → test → typecheck → lint
3. Push and open a PR; reference the issue with `Closes #[number]`

After pushing to a branch, provide these commands for local testing:

```bash
git fetch origin
git checkout <branch-name>
git pull origin <branch-name>
```

## Testing

- **Unit**: pure functions, utilities, isolated components
- **Integration**: API routes, DB operations
- **E2E**: critical user flows only (login, checkout, etc.)

Test files co-located with source: `utils/format.ts` → `utils/format.test.ts`

Always test: boundary conditions, error paths, business logic edge cases.
Skip: third-party internals, trivial getters, presentation-only snapshots.

Must pass before marking complete: `[TYPECHECK]` + `[TEST_ALL]` + `[LINT]` — zero errors.

## Design System

A `DESIGN.md` file at the project root defines the full visual design system for this project. For any UI or component work:

- **Colors**: Use palette names and hex values from DESIGN.md Section 2 — never hardcode arbitrary hex values
- **Typography**: Follow the type scale in Section 3 — sizes, weights, and line heights
- **Components**: Match the shapes, surfaces, and states described in Section 4
- **Spacing**: Use the base-unit grid from Section 5 — all spacing is a multiple of [4px or 8px]
- **Responsive**: Follow breakpoints and component adaptations in Section 8
- **Prompt help**: Section 9 provides copy-paste prompt fragments for common UI patterns

If `DESIGN.md` is not yet filled in for this project, ask before inventing visual decisions.

## Hard Rules

- Never commit `.env`, secrets, or credentials
- Never use `--no-verify`, `--force`, or skip lint/type checks
- Never force-push to shared branches
- Prefer editing existing files over creating new ones
- No error handling for scenarios that cannot happen
- No speculative abstractions — implement exactly what was asked
