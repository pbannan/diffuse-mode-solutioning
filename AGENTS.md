# Diffuse Mode Solutioning — Agent Instructions

> Self-contained agent instructions for this repository. Compatible with any AI coding agent (Claude, Copilot, Cursor, Codex, Gemini, etc.).

## Project

A minimal single-page app for sleep-powered problem-solving. Users set a focus problem before bed, log waking thoughts each morning, and surface patterns over time using Claude AI.

**Stack**: Vanilla React 18 (CDN) · JavaScript · localStorage · Claude Haiku · Hand-crafted CSS

## Commands

```bash
# No install step — no dependencies

# Dev (option 1): open directly
open index.html

# Dev (option 2): local server
python3 -m http.server 8080   # → localhost:8080

# No build, no typecheck, no lint, no test runner
```

## Source Layout

```
index.html    # entire application — all HTML, CSS, and JavaScript in one file
              #   CSS:   lines ~14–89  (global styles and component classes)
              #   JS:    lines ~94+    (React 18 via CDN, Babel standalone)
              #   HTML:  lines ~91–93  (<div id="root">)
```

## Architecture

- **Single-file app**: all HTML, CSS, and JavaScript lives in `index.html`
- **React via CDN**: `react@18`, `react-dom@18`, `@babel/standalone`, `marked@9` — no npm, no build
- **State**: React `useState` hooks only — no external state management
- **Persistence**: `localStorage` with base64-encoded JSON (UTF-8-safe via `b64enc`/`b64dec` helpers)
- **AI**: Direct `fetch` to `https://api.anthropic.com/v1/messages` using `claude-haiku-4-5-20251001`
- **Routing**: None — tab state is a `useState` string (`"tonight"`, `"morning"`, `"log"`)
- **No server, no auth, no external dependencies** beyond CDN scripts and Google Fonts

Key data shape:
```js
entry = {
  id, ts, text,              // night focus: id, timestamp, problem text
  editedTs, history,         // edit history array
  deleted, deletedAt,        // soft archive
  morningLogs: [{            // array of waking log entries
    id, ts, wakingThoughts,
    categories, ideas,
    relatedToFocus
  }]
}
```

Key constants (top of `<script>`):
- `STORAGE_KEY` — localStorage key for entries
- `API_KEY_STORAGE` — localStorage key for Anthropic API key
- `CATEGORIES` — waking thought category options
- `HAIKU_INPUT_COST_PER_M` / `HAIKU_OUTPUT_COST_PER_M` — token cost display

**Do not change**:
- The localStorage key names (`STORAGE_KEY`, `API_KEY_STORAGE`) — changing them orphans existing user data
- The `b64enc`/`b64dec` helpers — they handle UTF-8 correctly where `btoa`/`atob` would break
- The CDN URLs and versions — they are pinned intentionally

## Code Conventions

**Naming**:
- React components: `PascalCase` (all defined inside `App()` as inline JSX)
- Event handlers: `camelCase` verbs — `saveEntry`, `archiveEntry`, `restoreVersion`
- Constants: `SCREAMING_SNAKE_CASE` at the top of the script block
- CSS classes: `kebab-case` matching the `.class-name` selectors in the `<style>` block

**Style rules**:
- All CSS lives in the `<style>` block — no inline style objects unless unavoidable
- No Tailwind, no CSS-in-JS, no CSS modules
- New component classes go at the bottom of the `<style>` block
- Reuse existing classes before adding new ones

**API calls**:
- All Anthropic API calls use `fetch` with `anthropic-version: 2023-06-01`
- Always include `anthropic-dangerous-direct-browser-access: true` header
- Model is `claude-haiku-4-5-20251001` — do not upgrade without the user's explicit approval

**Commits**: `type(scope): short description` — types: `feat`, `fix`, `refactor`, `docs`, `chore`

**PRs / issue comments**: Write each paragraph as a single continuous line — no mid-sentence hard wraps. GitHub renders bare newlines as visible line breaks.

## Git Workflow

Branch naming: `type/short-description` — e.g., `feat/waking-tags`, `fix/archive-restore`

After pushing to a branch, provide these commands for local testing:

```bash
git fetch origin
git checkout <branch-name>
git pull origin <branch-name>
```

## Testing

No test framework. Validate all changes manually in-browser:
1. Open `index.html` (or `localhost:8080`) in Chrome/Safari/Firefox
2. Exercise the specific feature changed
3. Check localStorage persistence: refresh the page and confirm data survives
4. Test the API integration with a real key if AI output is affected
5. Check the browser console for errors — zero console errors before marking complete

## Hard Rules

- Never commit API keys, `.env` files, or `localStorage` exports
- Never add `npm`, `package.json`, or build tooling — the no-install constraint is intentional
- Never import from `node_modules` or ES module paths — CDN only
- All changes go in `index.html` — do not create new files unless explicitly asked
- Prefer editing existing CSS classes over adding new ones
- No speculative abstractions — implement exactly what was asked

## Design System

A `DESIGN.md` file at the project root defines the visual design system. For any UI work:

- **Colors**: Use palette names from DESIGN.md — the palette is monochromatic dark with a single Electric Mint accent
- **Typography**: IBM Plex Mono exclusively — all sizes, weights, and tracking values are in DESIGN.md Section 3
- **Components**: Match existing CSS class patterns — shapes are sharp (0px radius), spacing is tight
- **No new fonts or color values** without updating DESIGN.md first
