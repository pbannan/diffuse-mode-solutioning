# Conventions

## Naming

| Construct | Style | Example |
|-----------|-------|---------|
| React components | PascalCase | `MorningBlock`, `EntryRow` |
| Event handlers & functions | camelCase verbs | `saveEntry()`, `archiveEntry()`, `restoreVersion()` |
| Constants | SCREAMING_SNAKE_CASE | `STORAGE_KEY`, `CATEGORIES` |
| CSS classes | kebab-case | `.save-btn`, `.ghost-btn`, `.morning-block` |
| localStorage keys | kebab-case strings | `"nightly-focus-log"` |

## CSS Conventions

All styles live in the `<style>` block at the top of `index.html`. No inline style objects, no Tailwind, no CSS-in-JS.

- Reuse existing classes before adding new ones
- New classes go at the **bottom** of the `<style>` block
- Class names describe the component role, not the visual outcome (`.save-btn` not `.cream-button`)
- State variants use modifiers: `.ghost-btn.danger`, `.chip.selected`, `.tab.active`, `.entry.archived`
- Responsive overrides use `@media (hover: hover) and (pointer: fine)` for touch-device safety

## React Conventions

- All components are functions defined inline inside `App()` — no separate component files
- No class components, no `React.Component`
- Hooks at the top of `App()`, grouped by feature (Tonight / Morning / Log / Patterns)
- Event handlers defined as `const name = (...) => { ... }` closures inside `App()`
- JSX returned from `App()` uses conditional rendering with `&&` and ternary operators
- `key` props use stable IDs (`entry.id`, `waking.id`) — never array index

## JavaScript Style

- `const` for everything that doesn't need reassignment
- Arrow functions for handlers and helpers
- No `async/await` — use `.then()/.catch()` chains (consistent with existing code)
- Template literals for string interpolation
- Destructuring for state variables and props
- No optional chaining (`?.`) or nullish coalescing (`??`) in legacy sections — check existing usage first

## API Calls

- Always include `"anthropic-dangerous-direct-browser-access": "true"` header
- Always include `"anthropic-version": "2023-06-01"` header
- Model is `claude-haiku-4-5-20251001` — do not change without user approval
- Display token costs using `HAIKU_INPUT_COST_PER_M` / `HAIKU_OUTPUT_COST_PER_M` constants

## Commit Messages

Format: `type(scope): short description` — imperative mood, lowercase, no period, under 72 chars.

Types: `feat` · `fix` · `refactor` · `docs` · `chore`

Examples:
```
feat(morning): add multiple waking log entries per night
fix(log): restore archived entry clears deletedAt correctly
chore(deps): pin marked to v9 to avoid breaking API change
```

## PR and Issue Comment Formatting

Write each paragraph as a **single continuous line** with no embedded newlines. GitHub renders bare newlines as line breaks. Separate paragraphs with a blank line.
