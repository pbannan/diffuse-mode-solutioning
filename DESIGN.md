# DESIGN.md — [Project Name]

> Machine-readable design system for AI coding agents. Defines tokens, components, and visual rules so agents generate consistent UI without per-prompt style instructions.
>
> **Format**: Google Stitch DESIGN.md (9-section standard).
> **Rule**: Use descriptive language with precise values in parentheses. Avoid raw CSS class names (`rounded-xl`, `text-sm`) — use natural language ("gently curved 6px corners", "14px body text"). Avoid generic color names ("blue") — use descriptive names with hex values ("Midnight Indigo (#4F46E5)").

---

## 1. Visual Theme & Atmosphere

[2–3 sentences describing the overall mood, emotional tone, and design philosophy. Examples:]

- **Professional / dense**: "Clean, high-density interface built for power users who value information over decoration. Surfaces are minimal; whitespace is functional, not decorative. Every pixel earns its place."
- **Friendly / spacious**: "Warm, airy interface with generous breathing room. Approachable and trustworthy — designed to feel helpful, not demanding."
- **Dark / technical**: "Dark-first developer aesthetic with precise mechanical alignment. Prioritizes readability in low-light environments and signals technical sophistication."

**Density**: [Compact / Balanced / Spacious]
**Corner philosophy**: [Sharp (0px) / Subtle (2–4px) / Rounded (6–8px) / Very rounded (12–16px) / Pill]
**Visual weight**: [Lightweight / Medium / Bold]
**Motion**: [Minimal / Purposeful transitions only / Rich micro-interactions]

---

## 2. Color Palette & Roles

### Core Palette

| Role | Descriptive Name | Hex | Functional Purpose |
|------|-----------------|-----|-------------------|
| Primary | [e.g., Midnight Indigo] | `[#4F46E5]` | CTAs, links, active indicators |
| Primary hover | [e.g., Deep Indigo] | `[#4338CA]` | Interactive state on primary elements |
| Primary subtle | [e.g., Lavender Mist] | `[#EEF2FF]` | Selected rows, highlight backgrounds |
| Secondary | [e.g., Cool Slate] | `[#64748B]` | Secondary actions, supporting accents |
| Background | [e.g., Cloud White] | `[#FFFFFF]` | Page and layout background |
| Surface | [e.g., Soft Pearl] | `[#F8FAFC]` | Cards, panels, elevated containers |
| Surface raised | [e.g., Pale Silver] | `[#F1F5F9]` | Nested surfaces, hover states |
| Border | [e.g., Cool Gray] | `[#E2E8F0]` | Dividers, input strokes, outlines |
| Border strong | [e.g., Steel Gray] | `[#CBD5E1]` | Focused inputs, prominent dividers |
| Text primary | [e.g., Charcoal] | `[#0F172A]` | Headings, body copy |
| Text secondary | [e.g., Slate Gray] | `[#475569]` | Labels, metadata, captions |
| Text tertiary | [e.g., Light Slate] | `[#94A3B8]` | Placeholders, hints, timestamps |
| Text disabled | [e.g., Mist] | `[#CBD5E1]` | Inactive / read-only elements |
| Text on-primary | White | `[#FFFFFF]` | Text on primary-colored surfaces |

### Semantic / Feedback Colors

| Role | Descriptive Name | Hex | Surface Tint Hex | Usage |
|------|-----------------|-----|-----------------|-------|
| Success | [e.g., Forest Green] | `[#16A34A]` | `[#F0FDF4]` | Confirmations, completed states |
| Warning | [e.g., Amber] | `[#D97706]` | `[#FFFBEB]` | Caution, pending states |
| Destructive | [e.g., Crimson] | `[#DC2626]` | `[#FEF2F2]` | Errors, delete actions |
| Info | [e.g., Sky Blue] | `[#0284C7]` | `[#F0F9FF]` | Informational highlights |

### Dark Mode Overrides *(if applicable)*

| Role | Light | Dark |
|------|-------|------|
| Background | `[#FFFFFF]` | `[#09090B]` |
| Surface | `[#F8FAFC]` | `[#18181B]` |
| Surface raised | `[#F1F5F9]` | `[#27272A]` |
| Border | `[#E2E8F0]` | `[#3F3F46]` |
| Text primary | `[#0F172A]` | `[#FAFAFA]` |
| Text secondary | `[#475569]` | `[#A1A1AA]` |

---

## 3. Typography Rules

### Font Families

- **Primary**: [e.g., Inter] — used for all UI text, headings, and body copy
- **Monospace**: [e.g., JetBrains Mono] — code blocks, technical data, version numbers

*Fallback stack*: `"[Primary]", system-ui, -apple-system, sans-serif`

### Type Scale

| Role | Size | Weight | Line Height | Letter Spacing | Usage |
|------|------|--------|-------------|----------------|-------|
| Display | [40–48px] | 800 | 1.1 | −0.02em | Hero headlines only |
| Heading 1 | [30–36px] | 700 | 1.15 | −0.015em | Page titles |
| Heading 2 | [22–28px] | 600–700 | 1.25 | −0.01em | Section headers |
| Heading 3 | [18–22px] | 600 | 1.3 | 0 | Sub-headers, card titles |
| Heading 4 | [15–18px] | 600 | 1.4 | 0 | Tight sub-headers, table headers |
| Body large | [16–18px] | 400 | 1.6 | 0 | Lead paragraphs, feature text |
| Body | [14–16px] | 400 | 1.5 | 0 | Default body copy |
| Body small | [12–14px] | 400 | 1.45 | 0 | Supporting text, captions |
| Label | [11–13px] | 500–600 | 1.2 | 0.02–0.05em | UI labels, button text, badges |
| Code | [13px] | 400 | 1.65 | 0 | Inline code, code blocks |

---

## 4. Component Stylings

Describe appearance as a designer would — shape, surface, shadow, state transitions. No CSS class names.

### Buttons

**Primary**: [Primary color] background, white label text (Label size, medium-heavy weight). [Corner description, e.g., "gently rounded 6px corners"]. [Padding, e.g., "12px top/bottom, 20px left/right"]. No shadow at rest. Hover: slightly deeper shade ([Primary hover hex]). Active: further deepened with subtle inward shadow. Disabled: [Surface raised] background with [Text disabled] label, cursor not-allowed.

**Secondary**: Transparent background with a [1px Border stroke] outline. [Text primary] label. Hover: [Surface raised] background fills in. Active: border deepens to [Border strong].

**Destructive**: [Destructive color] background, white label. Same shape and size as primary. Hover: darkened destructive shade.

**Ghost / text**: No border, no background fill. [Primary color] label. Hover: [Primary subtle] background appears. Used for inline actions within content.

**Icon button**: Square or circle, [32–40px], same corner treatment. Tooltip required on all icon-only buttons.

### Input Fields

[Surface] background with [1px Border stroke], [corner description]. [11–12px] top/bottom padding, [12–16px] left/right padding. Placeholder text in [Text tertiary]. Focus: border transitions to [Primary color] with a [very subtle primary glow / no glow]. Error: border becomes [Destructive] with an error message below in [Destructive] text. Success: border becomes [Success]. Disabled: [Surface raised] background, [Text disabled] text.

### Cards & Containers

[Surface] background, [corner description], [border or "hairline border using Border color"]. [shadow description from Section 6]. Inner padding [16–24px]. Hover (if interactive): border subtly deepens, or shadow elevates one level. Selected state: [Primary subtle] background tint with [Primary] left border accent.

### Navigation — Sidebar

[Surface or white] background. Item: [Text secondary] label, [icon size] leading icon. Active item: [Primary subtle] background fill with [Primary] label and icon. Hover: [Surface raised] tint. Dividers between groups use [Border color]. Collapsed state shows icons only with tooltips.

### Navigation — Top Bar

[Surface or white] background with a bottom [Border] hairline. Brand mark on the left, primary actions on the right. Active nav item: [Primary] underline (2–3px) or [Primary subtle] pill. Height [48–64px].

### Badges / Tags

Compact pill shape, [4px horizontal padding, 2px vertical], [Label small (11–12px), medium weight]. Neutral: [Surface raised] background, [Text secondary] text. Semantic variants use feedback palette surface tints as background with the corresponding strong color for text.

### Modals & Dialogs

Backdrop: semi-transparent [dark overlay] (40–60% opacity). Panel: [Surface or white] background, [corner description, typically more rounded than cards], [Floating elevation shadow from Section 6]. Max-width [480–640px], full-width on mobile with rounded top corners and flat bottom (bottom sheet). Closes on backdrop click and Escape key. Focus trapped inside while open.

### Tables

Header row: [Surface raised] background, [Text secondary] label text (Label size, medium weight), [8–12px] vertical padding. Body rows: alternating white / [Surface] background, or single color with [Border] horizontal dividers between rows. [12–14px] vertical padding per row. Hover: [Surface raised] tint on the hovered row. Selected: [Primary subtle] background.

---

## 5. Layout Principles

### Spacing Scale

Base unit: **[4px or 8px]**. All spacing values are multiples of the base unit.

| Token | Value | Typical Usage |
|-------|-------|---------------|
| xs | 4px | Inline gaps, icon-to-label spacing |
| sm | 8px | Tight groupings, compact padding |
| md | 16px | Component internal padding |
| lg | 24px | Between related elements |
| xl | 32px | Section separators |
| 2xl | 48px | Major section breaks |
| 3xl | 64–96px | Page-level top/bottom padding |

### Grid & Container

- **Max content width**: [1280–1440px], centered
- **Gutters**: [16px] mobile, [24px] tablet, [32px] desktop
- **Column grid**: 12 columns on desktop, 8 on tablet, 4 on mobile
- **Sidebar width**: [240–280px] (if applicable)

### Whitespace Strategy

[Describe the philosophy, e.g.: "Cards use 24px inner padding for a roomy feel. Sections breathe with 48px vertical gaps. Inline elements and list items use 8px spacing. Dense data views (tables, logs) use 12px row padding to maximize information density."]

---

## 6. Depth & Elevation

Describe with evocative language alongside technical values.

| Level | Description | CSS Shadow Value | Usage |
|-------|-------------|-----------------|-------|
| Flat | No depth | none | Default containers, flush-to-surface elements |
| Raised | Whisper of depth | `0 1px 3px rgba(0,0,0,0.08), 0 1px 2px rgba(0,0,0,0.04)` | Cards, list items, interactive surfaces |
| Lifted | Clear separation | `0 4px 12px rgba(0,0,0,0.10), 0 2px 4px rgba(0,0,0,0.06)` | Dropdowns, popovers, date pickers |
| Floating | Prominent elevation | `0 8px 24px rgba(0,0,0,0.14), 0 4px 8px rgba(0,0,0,0.08)` | Modals, dialogs, command palettes |
| Pinned | Directional depth | `0 2px 8px rgba(0,0,0,0.12)` | Sticky headers, fixed bottom bars |

**Dark mode elevation**: On dark surfaces, prefer lighter surface colors over shadows to indicate elevation — shadows lose definition against dark backgrounds.

---

## 7. Do's and Don'ts

### Do
- Reference palette names (e.g., "Midnight Indigo") in designs; the hex is an implementation detail
- Follow the [4px or 8px] spacing grid — all spacing values must be multiples of the base unit
- Left-align body text; center only short UI labels and isolated CTAs
- Reserve [Primary color] for one focused action per screen — it loses meaning when overused
- Apply visible focus rings on every interactive element (keyboard accessibility is non-negotiable)
- Pair status colors with icons or labels — never rely on color alone to communicate state
- Use the destructive color only for genuinely irreversible actions

### Don't
- Mix more than two typefaces on one screen
- Use opacity to create "disabled" text — use the explicit [Text disabled] token
- Apply decorative shadows to flat designs — choose a consistent elevation story and maintain it
- Place destructive actions adjacent to primary CTAs without visual separation or a confirmation step
- Use fully saturated pure black (`#000000`) or pure white (`#FFFFFF`) for text on backgrounds
- Hardcode hex values in components — always reference design tokens
- Add new colors outside the palette without updating this file first

---

## 8. Responsive Behavior

### Breakpoints

| Name | Min Width | Layout |
|------|-----------|--------|
| Mobile | 0 | Single column, full-width components, stacked navigation |
| Tablet (sm) | [640px] | Two columns for cards/grids; side panels collapse to drawers |
| Tablet (md) | [768px] | Navigation may shift from bottom bar to side panel |
| Desktop | [1024px] | Full layout, sidebar permanently visible |
| Wide | [1280px+] | Max-width container centered; no further layout change |

### Touch Targets

Minimum tap target: **44×44px** on mobile. Increase padding rather than altering visual size to meet this requirement. Interactive elements should not be placed within 8px of each other on touch surfaces.

### Navigation Patterns

- **Desktop**: [e.g., Persistent left sidebar]
- **Tablet**: [e.g., Collapsible sidebar, toggle via hamburger]
- **Mobile**: [e.g., Bottom navigation bar for primary items, full-screen drawer for secondary]

### Component Adaptations

- **Cards**: [X] per row on desktop → [Y] on tablet → 1 column stacked on mobile
- **Tables**: Horizontal scroll on mobile; consider card-per-row fallback for dense tables
- **Modals**: Full-height bottom sheet on mobile (rounded top corners, flat bottom)
- **Sidebar**: Hidden by default on mobile; slides in from the left as a full-height drawer

---

## 9. Agent Prompt Guide

Copy-paste fragments for generating UI consistent with this design system.

### Color Reference Cheatsheet

```
Primary:          [Descriptive Name] ([#hex])
Primary hover:    [Descriptive Name] ([#hex])
Primary subtle:   [Descriptive Name] ([#hex])
Background:       [Descriptive Name] ([#hex])
Surface:          [Descriptive Name] ([#hex])
Border:           [Descriptive Name] ([#hex])
Text primary:     [Descriptive Name] ([#hex])
Text secondary:   [Descriptive Name] ([#hex])
Success:          ([#hex])  |  Warning: ([#hex])  |  Error: ([#hex])
```

### Reusable Prompt Fragments

**New screen or page**:
> "Build [screen name] following DESIGN.md. Use [Background name] as the page background. Content lives in [Surface name] cards with [corner description] and [elevation level] shadow. All typography follows Section 3's type scale. Navigation uses the [sidebar / top bar] pattern from Section 4."

**Form UI**:
> "Create [form name]. Inputs use [Surface] background with [1px Border stroke], focused state uses a [Primary] border. Submit button is primary style. Show inline validation: [Destructive] border + message below on error, [Success] border on valid. Disabled fields use [Surface raised] with [Text disabled] label."

**Data table or list**:
> "Build a [table / list] displaying [data type]. Rows use [Body small] text, [12px] vertical padding, [Border] dividers. Header row has [Surface raised] background with [Label] text. Hover row highlights with [Surface raised] tint. Selected row uses [Primary subtle] background with a [Primary] left-border accent."

**Dashboard or data display**:
> "Create a dashboard card showing [metric]. Card uses [Surface] background, [Raised elevation], [corner description]. Heading in [Heading 3] style, value in [Display or Heading 1] style using [Text primary]. Supporting text in [Text secondary]. Use [Success] / [Destructive] for positive / negative trend indicators."

**Empty state**:
> "Design an empty state for [feature]. Centered layout, [Text secondary] headline at [Heading 3] size, [Text tertiary] supporting copy at [Body] size. Icon or illustration placeholder above the text. Optional primary CTA button below."

**Navigation component**:
> "Build a [sidebar / top nav] following DESIGN.md Section 4. Active item uses [Primary subtle background + Primary label]. Inactive items use [Text secondary]. Hover uses [Surface raised] tint. Include [icon + label] pairs. On mobile, [collapse pattern from Section 8]."
