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

---

## GitHub MCP Tools — Availability and Retries

The GitHub MCP server runs with `MCP_CONNECTION_NONBLOCKING=true`, which means the session starts before the server finishes connecting. Tools may not be available immediately. The `gh` CLI and `hub` CLI are **not** available in this environment.

**At the start of any task that needs GitHub tools**, always call ToolSearch with `"query": "mcp__github"` proactively — before you need a specific tool. This gives the MCP server time to finish connecting and surfaces the tool schemas early.

**If a tool call fails or ToolSearch returns no results:**
1. Wait a moment, then retry ToolSearch once more.
2. If tools are still unavailable after two ToolSearch attempts:
   - **For reading** an issue or PR: use `WebFetch` on the GitHub HTML URL (e.g. `https://github.com/pbannan/diffuse-mode-solutioning/issues/33`). This works for public repos and is not rate-limited like the REST API.
   - **For writing** (commenting, closing, creating PRs): there is no authenticated shell fallback. Tell the user: *"The GitHub MCP server is not responding. Please start a new session and try again."*
   - Do not use `curl` against `api.github.com` — unauthenticated API calls are limited to 60 requests/hour and the quota is often already exhausted.

## Closing GitHub Issues with the MCP Tools

Do **not** comment on or close an issue after pushing. There may be many pushes with their own commit messages — duplicate issue comments are not needed.

Wait until the user explicitly asks you to close the issue. That means the user has tested locally, approved the PR, and is ready to wrap up.

When the user asks you to close the issue, first run ToolSearch for `"mcp__github"` to ensure the tools are loaded, then do both steps below in order. If tools remain unavailable after retrying per the instructions above, report failure to the user.

### Step 1 — Comment with a summary of final changes and root cause

Use `mcp__github__add_issue_comment`:
- `owner`: `pbannan`
- `repo`: `diffuse-mode-solutioning`
- `issue_number`: the issue number
- `body`: a summary of the root cause and the final changes made to fix it

### Step 2 — Close the issue

Use `mcp__github__issue_write`:
- `owner`: `pbannan`
- `repo`: `diffuse-mode-solutioning`
- `issue_number`: the issue number
- `method`: `update`
- `state`: `closed`
- `state_reason`: `completed`
