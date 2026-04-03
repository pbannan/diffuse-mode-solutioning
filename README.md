# Diffuse Mode Solutioning

A minimal, single-page app for harnessing the problem-solving power of sleep.

## What it does

Each night, you write down the one problem you want your brain to work on overnight. Each morning, you log what you were thinking about when you woke up — capturing waking thoughts, categorizing them, and noting any ideas that surfaced. Over time, a log builds up that you can analyze for patterns using Claude AI.

**Three views:**

- **Tonight** — Set your focus problem before bed
- **Morning** — Log your waking thoughts and whether they connected back to your focus
- **Log** — Review your full history; archive entries; restore past versions; surface patterns with AI

## Inspiration

The name comes from Barbara Oakley's concept of **diffuse mode thinking** — the relaxed, background mental state (during sleep, exercise, daydreaming) where the brain makes unexpected connections and solves problems it couldn't crack through focused effort alone.

The practice is simple: give your subconscious a specific problem before you go to sleep. Don't force it. Wake up and write down whatever's on your mind before the day crowds it out. Over weeks, patterns emerge — about what actually has your attention, what domains you return to, and what your brain is quietly working through.

## How to use it

Open `index.html` in any browser. Everything runs locally — no server, no build step, no account. Your entries are saved to `localStorage` in your browser.

To unlock **pattern analysis**, you need an [Anthropic API key](https://console.anthropic.com/). Enter it in the Log tab; it's stored locally and only ever sent to Anthropic's API.

## Stack

- Vanilla HTML + React 18 (via CDN)
- IBM Plex Mono
- No build tooling, no dependencies to install
- Claude (Haiku) for pattern analysis
