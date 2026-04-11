# Testing

## No Test Framework

This project has no automated test runner, no Jest, no Vitest, no testing library. All validation is manual, in-browser.

## Manual Testing Checklist

Run through these steps after every change before marking a task complete:

### Core flow
- [ ] Open `index.html` in a browser (Chrome recommended; also spot-check Safari/Firefox)
- [ ] **Tonight tab**: type a focus problem → Save → confirm it appears at the top of the Log
- [ ] **Morning tab**: add a waking log entry with categories and ideas → Save → confirm it appears under the night entry in Log
- [ ] **Log tab**: edit a night entry → confirm history entry is created → restore a version
- [ ] Archive an entry → confirm it disappears (or appears dimmed with "show archived" toggle)

### Persistence
- [ ] After making changes, hard-refresh the page (`Cmd+Shift+R` / `Ctrl+Shift+R`)
- [ ] Confirm all data survives the reload (localStorage round-trip)
- [ ] Open DevTools → Application → Local Storage → verify data is base64-encoded JSON

### API integration (if AI output is affected)
- [ ] Enter a real Anthropic API key in the Log tab
- [ ] Run a pattern analysis and confirm the response renders as formatted Markdown
- [ ] Confirm cost display updates after the call completes
- [ ] Test with no API key — confirm the button is disabled or shows a clear error

### Error states
- [ ] Check the browser console: **zero errors and zero warnings** before marking complete
- [ ] Confirm nothing breaks when localStorage is empty (first-time user)

## Regression Areas to Watch

Changes in one area often break these unexpectedly:

- **Entry persistence**: Any change to the entry data shape must handle legacy entries (morningLog singular → morningLogs array migration in `getMorningLogs()`)
- **Base64 encoding**: Entries with emoji or non-ASCII characters must survive encode/decode
- **Archive toggle**: Archived entries must not appear in Morning tab's "tonight's focus" query
- **Category chips**: Custom tags ("Other") must persist alongside standard CATEGORIES selections
- **Pattern caching**: `PATTERNS_STORAGE` cache keyed on time box value — changing the key orphans cached results

## Before Marking Complete

1. All manual checklist steps above pass
2. Zero browser console errors
3. Data persists across hard refresh
4. The changed feature works on mobile viewport (375px width minimum)
