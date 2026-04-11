# DESIGN.md — Diffuse Mode Solutioning

> Machine-readable design system for AI coding agents. All values are extracted directly from `index.html`'s `<style>` block.
>
> **Rule**: Use descriptive color names with hex values in parentheses. Avoid raw CSS class names — describe appearance in natural language so any agent can interpret it correctly.

---

## 1. Visual Theme & Atmosphere

Dark, minimal, terminal-adjacent interface designed for quiet daily rituals — bedtime reflection and morning capture. The palette is near-monochromatic dark with warm cream text and a single Electric Mint accent reserved exclusively for AI-powered actions. There is no decoration: no shadows, no gradients, no border radii. Every element is flush, flat, and purposeful.

**Density**: Compact — tight spacing, small type, maximum content per screen
**Corner philosophy**: Sharp — 0px border-radius everywhere (2px only on the scrollbar thumb)
**Visual weight**: Lightweight — thin borders, muted grays, restrained hierarchy
**Motion**: Minimal — single fade-in animation (`opacity 0 → 1, translateY 4px → 0, 0.3s ease`) for new entries; 0.15–0.2s transitions on interactive states only

---

## 2. Color Palette & Roles

### Core Palette

| Role | Descriptive Name | Hex | Functional Purpose |
|------|-----------------|-----|-------------------|
| Background | Void Black | `#0d0d0d` | Page background (`body`) |
| Surface | Dark Charcoal | `#111111` | Text areas, inputs, panels, key input |
| Surface deep | Ink | `#0f0f0f` | Morning blocks, nested containers |
| Surface raised | Graphite | `#161616` | History items, selected chip background |
| Border subtle | Shadow | `#1a1a1a` | Entry dividers, privacy panel inner borders |
| Border | Dim | `#1e1e1e` | Input borders, text area borders, morning block left accent |
| Border medium | Ash | `#2a2a2a` | Scrollbar thumb, focused text area border |
| Border strong | Slate | `#333333` | Chip borders, toggle boxes, key input focus |
| Border hover | Steel | `#555555` | Hovered chip borders |
| Text primary | Warm Cream | `#e8e4d9` | Main body text, active tab, save button background |
| Text secondary | Pewter | `#777777` | Inactive tabs, secondary labels, datetime inputs |
| Text tertiary | Stone | `#666666` | Field labels, ghost buttons, insight MD headings |
| Text muted | Dusk | `#555555` | Inline buttons, disabled states |
| Text disabled | Fog | `#444444` | Tag input placeholder text |
| Text accent | Burnished Cream | `#c8c4b8` | Selected chip text, toggle checkmark |
| Text on-dark | Near Black | `#0a0a0a` | Text on Electric Mint (insight button) |
| Text on-primary | Near Black | `#0d0d0d` | Text on Warm Cream (save button) |
| Insight text | Warm Stone | `#9a9690` | AI output markdown — strong, headings |

### Semantic / Feedback Colors

| Role | Descriptive Name | Hex | Usage |
|------|-----------------|-----|-------|
| Primary action | Electric Mint | `#4ade80` | Insight / pattern analysis button — the only bright accent |
| Primary action hover | Bright Mint | `#6aee90` | Hover state on insight button |
| Danger | Muted Crimson | `#8a4a4a` | Ghost button danger hover (archive, delete actions) |

### Dark Mode

This app is dark-mode only. There are no light mode overrides.

---

## 3. Typography Rules

### Font Family

- **Only font**: IBM Plex Mono (weights 300, 400, 500) — loaded from Google Fonts
- Applied to: everything — body, inputs, buttons, labels, code

*Fallback stack*: `'IBM Plex Mono', monospace`

There is intentionally no secondary or display font. The monospace aesthetic is core to the product identity.

### Type Scale

All sizes are small; the app is information-dense and terminal-adjacent.

| Role | Size | Weight | Line Height | Letter Spacing | Usage |
|------|------|--------|-------------|----------------|-------|
| Body / textarea | 13px | 400 | 1.7 | 0 | Main text entry (`.text-area`) |
| Key input | 12px | 400 | — | 0.04em | API key field (`.key-input`) |
| Save button | 12px | 400 | — | 0.10em | Primary action label (`.save-btn`) |
| Insight button | 11px | 500 | — | 0.08em | AI action label (`.insight-btn`) |
| Tab | 11px | 400 | — | 0.12em | Navigation tabs (`.tab`), uppercase |
| Privacy panel | 11px | 400 | 1.65 | 0 | Data export preview |
| Ghost / chip / label | 10px | 400–500 | 1 | 0.08–0.14em | Buttons, chips, field labels (`.ghost-btn`, `.chip`, `.field-label`) |
| Tag input | 10px | 400 | — | 0.08em | Custom tag entry (`.tag-input`) |

All text-transform: uppercase is used sparingly — tabs, ghost buttons, field labels only.

---

## 4. Component Stylings

Describe appearance as a designer would — shape, surface, states. No CSS class names in design descriptions.

### Primary Button (Save)

Warm Cream (`#e8e4d9`) background, Near Black (`#0d0d0d`) text. 12px monospace, 0.10em letter spacing. No border, no border-radius — fully sharp corners. Padding: 10px top/bottom, 28px left/right. Hover: opacity drops to 85% (no color change). Disabled: opacity 40%, cursor not-allowed.

### AI Action Button (Insight / Analyze)

Electric Mint (`#4ade80`) background, Near Black (`#0a0a0a`) text, 500 weight. 11px, 0.08em letter spacing. Sharp corners. Padding: 10px top/bottom, 24px left/right. Hover: Bright Mint (`#6aee90`) background. Disabled: opacity 35%, cursor not-allowed. This is the only green element in the entire interface — it signals "AI-powered action."

### Ghost Button

Transparent background and border. Stone (`#666`) text, 10px, uppercase, 0.10em letter spacing. Hover variants: neutral hover → Pewter (`#888`); danger hover → Muted Crimson (`#8a4a4a`); accent hover → Warm Cream (`#e8e4d9`).

### Inline Button

Minimal: transparent, no border. Dusk (`#555`) text, 10px, 0.08em letter spacing. Hover: Pewter (`#999`). Used for secondary in-context actions.

### Text Area / Input

Dark Charcoal (`#111`) background, Dim (`#1e1e1e`) border (1px solid), Warm Cream (`#e8e4d9`) text. 13px body / 14px top-bottom 16px left-right padding. Line height 1.7. Focus: border lightens to Ash (`#2a2a2a`), no glow. No border-radius.

### API Key Input

Same surface as text area — Dark Charcoal background, Dim border. Warm Cream text. 12px, 0.04em tracking. 10px 14px padding. Focus: border becomes Slate (`#333`).

### Tag Input

No background, no border — only a bottom border using Shadow (`#222`). Pewter text, 10px, 0.08em. Placeholder in Fog (`#444`). Focus: bottom border lightens to Steel (`#444`). Width: 120px fixed.

### Category Chips

Transparent background with Slate (`#333`) border (1px solid). Pewter (`#777`) text, 10px, 0.08em. 4px top/bottom, 10px left/right padding. 3px margin between chips. No border-radius — fully square. Hover (pointer devices only): border to Steel (`#555`), text to Light Gray (`#aaa`). Selected state: Graphite (`#161616`) background, Slate (`#666`) border, Burnished Cream (`#c8c4b8`) text.

### Navigation Tabs

Transparent background with a 1px bottom border as the active indicator. Stone (`#777`) text, 11px, uppercase, 0.12em letter spacing. 6px top/bottom padding. Active: Warm Cream (`#e8e4d9`) text + Warm Cream bottom border. Hover: Pewter (`#999`). Transition 0.2s.

### Log Entries

Separated by a Shadow (`#1a1a1a`) bottom border (1px). 20px top/bottom padding. Fade-in animation on appearance. Archived entries: 40% opacity.

### Morning Block

Ink (`#0f0f0f`) background. Dim (`#1e1e1e`) left border accent (1px). 12px top/bottom, 14px left/right padding. 14px top margin. Fade-in animation on expansion.

### History Items

10px top/bottom padding. Very Dark (`#161616`) bottom border. Flex row with 12px gap.

### Toggle (Checkbox)

14×14px box, Slate (`#333`) border (1px solid). Checked state: Graphite (`#1a1a1a`) background, Slate (`#666`) border, × symbol in Burnished Cream (`#c8c4b8`) at 11px. No border-radius.

### Privacy / Data Panel

Dark Charcoal (`#111`) background, Shadow (`#1a1a1a`) border. Fade-in animation. Pre-formatted text in Stone (`#666`), 11px, 1.65 line height, `pre-wrap`, max-height 220px with scroll.

### AI Markdown Output

No background or border. Headings and `strong` in Warm Stone (`#9a9690`), weight 500, inherit font-size. `em` is italic. Lists use 1.4em left padding, 0.75em bottom margin. Paragraphs: 0.75em bottom margin.

---

## 5. Layout Principles

### Spacing

There is no formal spacing scale — spacing is set per component. Observed values:

| Context | Value |
|---------|-------|
| Entry vertical padding | 20px top/bottom |
| Tab vertical padding | 6px top/bottom |
| Text area / input padding | 14px 16px |
| Button padding (save) | 10px 28px |
| Button padding (insight) | 10px 24px |
| Chip padding | 4px 10px |
| Chip gap | 3px |
| Morning block padding | 12px 14px |
| Morning block top margin | 14px |
| History item padding | 10px 0 |
| History item gap | 12px |

### Grid & Container

No grid system — the app is single-column. The container width is managed via inline styles in JSX (check `App()` return for `style={{ maxWidth, padding }}`). On mobile: full-width, single column.

### Scrollbar

Width: 4px. Track: transparent. Thumb: Ash (`#2a2a2a`), 2px border-radius (the only rounded element in the UI).

---

## 6. Depth & Elevation

This app is **flat** — no shadows are used. Depth and hierarchy are communicated through:

- **Color contrast**: darker surfaces for nested containers (morning blocks inside entries)
- **Borders**: thin 1px borders delineate surfaces rather than shadows
- **Left border accent**: `border-left: 1px solid #1e1e1e` on morning blocks signals nesting
- **Opacity**: archived entries at 40% opacity recede visually

| Level | Method | Usage |
|-------|--------|-------|
| Flat | No shadow, no border | Most containers, page background |
| Nested | Darker background (`#0f0f0f`) + left border | Morning blocks inside log entries |
| Inset | Very dark background + border | Text areas, inputs |
| Receded | 40% opacity | Archived entries |

---

## 7. Do's and Don'ts

### Do
- Use Warm Cream (`#e8e4d9`) for primary interactive elements (save buttons, active state text)
- Reserve Electric Mint (`#4ade80`) exclusively for AI-powered actions — it is the only bright color
- Use the existing `.ghost-btn`, `.inline-btn` classes for secondary actions rather than creating new button styles
- Keep all text in IBM Plex Mono — it is a core part of the product identity
- Use opacity (40%) for archived/disabled states on containers rather than background color changes
- Keep borders at 1px solid — never thicker

### Don't
- Add border-radius to any interactive element — the sharp aesthetic is intentional
- Add shadows or gradients — this design is deliberately flat
- Introduce any new font — IBM Plex Mono exclusively
- Use pure white (`#ffffff`) or pure black (`#000000`) — use Warm Cream and Void Black instead
- Add a second accent color — Electric Mint must remain the only bright element
- Increase font sizes beyond 13px for body text — the compact density is intentional
- Use color alone to communicate state — pair color changes with cursor or opacity changes

---

## 8. Responsive Behavior

### Breakpoints

The app has minimal responsive handling. Primary target is a narrow single-column view.

| Context | Behavior |
|---------|----------|
| Touch devices | Chip hover states are disabled via `@media (hover: hover) and (pointer: fine)` |
| Mobile | Full-width single column; no layout shift |
| Desktop | Same layout, naturally wider |

No explicit breakpoints for layout change — the single-column design adapts naturally.

### Touch Targets

All buttons use sufficient padding for touch (10px+ vertical). Category chips are 4px vertical — borderline on mobile; avoid reducing further.

### Navigation

Three tabs (`Tonight` / `Morning` / `Log`) displayed horizontally at all screen sizes. No hamburger menu, no drawer.

---

## 9. Agent Prompt Guide

### Color Reference Cheatsheet

```
Page background:    Void Black (#0d0d0d)
Input surface:      Dark Charcoal (#111111)
Nested container:   Ink (#0f0f0f)
Border default:     Dim (#1e1e1e)
Border strong:      Slate (#333333)
Text primary:       Warm Cream (#e8e4d9)
Text secondary:     Pewter (#777777)
Text label:         Stone (#666666)
Text selected:      Burnished Cream (#c8c4b8)
AI accent:          Electric Mint (#4ade80) — ONLY for AI-powered actions
AI accent hover:    Bright Mint (#6aee90)
Danger:             Muted Crimson (#8a4a4a)
AI output text:     Warm Stone (#9a9690)
```

### Reusable Prompt Fragments

**New input or text field**:
> "Add a text input using the existing `.text-area` or `.key-input` class pattern — Dark Charcoal (#111) background, Dim (#1e1e1e) 1px border, Warm Cream (#e8e4d9) text, IBM Plex Mono, sharp corners. Focus state: border lightens to Ash (#2a2a2a)."

**New action button (non-AI)**:
> "Add a primary action button using the `.save-btn` pattern — Warm Cream (#e8e4d9) background, Near Black (#0d0d0d) text, 12px IBM Plex Mono, 0.10em letter spacing, sharp corners, 10px 28px padding. Hover: opacity 85%."

**New AI-powered button**:
> "Add an AI action button using the `.insight-btn` pattern — Electric Mint (#4ade80) background, Near Black (#0a0a0a) text, 11px IBM Plex Mono weight 500, sharp corners, 10px 24px padding. Hover: Bright Mint (#6aee90) background. This is the only bright green element in the UI."

**New section or container**:
> "Add a container using the `.morning-block` pattern — Ink (#0f0f0f) background, Dim (#1e1e1e) left border (1px), 12px 14px padding, with the fade-in animation. No shadows, no border-radius."

**New label or field header**:
> "Add a field label using the `.field-label` pattern — Stone (#666666), 10px IBM Plex Mono, 0.14em letter spacing, uppercase, 10px bottom margin."

**New navigation or tab item**:
> "Add a tab using the `.tab` pattern — Stone (#777) text, 11px uppercase IBM Plex Mono, 0.12em tracking, 6px vertical padding. Active state: Warm Cream (#e8e4d9) text + 1px bottom border in Warm Cream. No background change."
