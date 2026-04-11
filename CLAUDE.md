# Diffuse Mode Solutioning

A minimal single-page app for sleep-powered problem-solving. Set a focus problem before bed, log waking thoughts each morning, and surface patterns over time using Claude AI.

## Stack

- **Framework**: Vanilla React 18 (loaded via CDN — no npm, no build step)
- **Language**: JavaScript (no TypeScript, no transpilation beyond Babel CDN)
- **Persistence**: localStorage (base64-encoded JSON — no server, no database)
- **AI**: Claude Haiku (`claude-haiku-4-5-20251001`) via direct Anthropic API fetch
- **Styling**: Hand-crafted CSS + IBM Plex Mono (Google Fonts)
- **Deploy**: Static file — open `index.html` directly in any browser

## Commands

```bash
# No install step — no dependencies

# Dev (option 1): open directly
open index.html

# Dev (option 2): local server to avoid CORS issues
python3 -m http.server 8080   # → localhost:8080

# No build, no typecheck, no lint, no test runner
```

## Source Layout

```
index.html    # entire application — all HTML, CSS, and JavaScript in one file
              #   CSS:   lines ~14–89  (global styles and component classes)
              #   JS:    lines ~94+    (React components, state, API calls)
              #   HTML:  lines ~91–93  (<div id="root">)
```

## Non-Negotiable Rules

- Never commit API keys, localStorage data, or anything from `.env`
- All changes go in `index.html` — do not create new files unless explicitly asked
- Preserve the no-build-step constraint: no npm imports, no ES modules, CDN only
- Test in-browser after every change — there is no test suite or type checker

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
