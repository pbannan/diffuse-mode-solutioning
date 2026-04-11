# Architecture

## File Structure

```
index.html    # entire application — do not split into separate files
              #   <style>  lines ~14–89   global CSS and component classes
              #   <body>   lines ~91–93   <div id="root"> only
              #   <script type="text/babel">  lines ~94+  all React code
```

## Single-File React App

This is a deliberate constraint: the app runs by opening `index.html` in a browser. There is no build step, no npm, no server.

**CDN dependencies (do not change versions without explicit approval)**:
- `react@18` + `react-dom@18` — via unpkg
- `@babel/standalone` — transpiles JSX in the browser at runtime
- `marked@9` — Markdown rendering for AI output
- IBM Plex Mono — Google Fonts

## State Architecture

All state lives in the single `App()` component via `useState`. There is no global store, no context, no reducer.

Key state groups:
- **View routing**: `view` (`"tonight"` | `"morning"` | `"log"`)
- **Tonight**: `nightInput`, `nightSaved`
- **Morning**: `wakingDraft`, `editingWakingId`, `wakingCustomTag`, `wakingShowOther`, `wakingSaved`
- **Log editing**: `editingId`, `editDraft`, `editDatetime`, `editingLogWaking`, `logWakingDraft`
- **Log display**: `expandedHistory`, `showArchived`
- **Patterns**: `insight`, `loadingInsight`, `insightError`, `timeBox`, `cachedPatterns`
- **API key**: `apiKey`, `rememberKey`

## Data Model (localStorage)

```js
// Entry (night focus + morning logs)
{
  id: string,           // uuid-like timestamp
  ts: string,           // ISO timestamp of creation
  text: string,         // night focus problem
  editedTs?: string,    // ISO timestamp of last edit
  history?: [{text, ts}],  // edit history
  deleted?: boolean,    // soft-archived
  deletedAt?: string,
  morningLogs?: [{
    id: string,
    ts: string,
    wakingThoughts: string,
    categories: string[],  // from CATEGORIES constant
    ideas: string,
    relatedToFocus: boolean
  }]
}
```

Stored as `localStorage.setItem(STORAGE_KEY, b64enc(JSON.stringify(entries)))`.

The `b64enc`/`b64dec` helpers are UTF-8-safe wrappers around `btoa`/`atob`. Do not replace them.

## AI Integration

```js
// Direct browser fetch — no proxy, no backend
fetch("https://api.anthropic.com/v1/messages", {
  method: "POST",
  headers: {
    "x-api-key": apiKey,
    "anthropic-version": "2023-06-01",
    "anthropic-dangerous-direct-browser-access": "true",
    "content-type": "application/json"
  },
  body: JSON.stringify({
    model: "claude-haiku-4-5-20251001",
    max_tokens: 1024,
    messages: [{ role: "user", content: prompt }]
  })
})
```

The API key is user-supplied, stored optionally in localStorage under `API_KEY_STORAGE`.

## Do Not Touch

- `STORAGE_KEY` and `API_KEY_STORAGE` constants — changing them orphans user data
- `b64enc` / `b64dec` functions — they handle multi-byte characters correctly
- CDN `<script>` tag versions — they are intentionally pinned
- The single-file constraint — do not extract files without explicit instruction
