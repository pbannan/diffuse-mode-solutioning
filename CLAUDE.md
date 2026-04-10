# [PROJECT_NAME]

[One to two sentences describing what this project does and who it serves.]

## Stack

- **Framework**: [e.g., Next.js 14 — App Router]
- **Language**: [e.g., TypeScript 5 strict]
- **Database**: [e.g., PostgreSQL via Prisma]
- **Auth**: [e.g., NextAuth.js v5]
- **Styling**: [e.g., Tailwind CSS v3]
- **Deploy**: [e.g., Vercel + GitHub Actions]

## Commands

```bash
[INSTALL]         # e.g., pnpm install
[DEV]             # e.g., pnpm dev  →  localhost:3000
[TEST_SINGLE]     # e.g., pnpm test -- -t "test name"
[TEST_ALL]        # e.g., pnpm test
[TYPECHECK]       # e.g., pnpm typecheck
[LINT]            # e.g., pnpm lint:fix
[BUILD]           # e.g., pnpm build
[MIGRATE]         # e.g., pnpm prisma migrate dev
```

## Source Layout

```
src/
  app/          # routes & pages
  components/   # shared UI components
  lib/          # third-party configs (singletons)
  utils/        # pure helpers (no side effects)
  hooks/        # custom React hooks
  types/        # TypeScript type definitions
```

## Non-Negotiable Rules

- Never commit `.env`, secrets, or credentials
- Run `[TYPECHECK]` and `[TEST_ALL]` before marking any task complete
- Prefer editing existing files over creating new ones
- No speculative abstractions — implement what is asked, nothing more

## Detailed Instructions

@.claude/instructions/architecture.md
@.claude/instructions/conventions.md
@.claude/instructions/git-workflow.md
@.claude/instructions/testing.md

## Design System

For any UI or component work, reference @DESIGN.md for colors, typography, spacing, and component conventions.
