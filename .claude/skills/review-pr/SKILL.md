---
name: review-pr
description: Reviews a pull request for correctness, conventions, and security. Delegates to specialized subagents and posts a consolidated review. Usage: /review-pr <pr-number>
disable-model-invocation: true
---

Review pull request: $ARGUMENTS

Steps:
1. Read the PR: `gh pr view $ARGUMENTS` — understand intent and scope
2. Inspect all changes: `gh pr diff $ARGUMENTS`
3. Use the `code-reviewer` subagent for correctness, conventions, and maintainability
4. Use the `security-reviewer` subagent for vulnerability analysis
5. Consolidate findings — remove duplicates, rank by severity
6. Post a structured review comment with sections:
   - **Must Fix** — blocks merging
   - **Should Fix** — address in this PR
   - **Consider** — optional future improvements
   - **Looks Good** — specific strengths (be concrete)

Formatting rules for the review comment:
- Write each paragraph as a single continuous line — no mid-sentence hard wraps
- Quote file path and line number for every specific issue (`src/api/users.ts:42`)
- Be precise: name the vulnerability or bug, don't just say "validate input"
- If a section is empty, omit it
