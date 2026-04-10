---
name: fix-issue
description: End-to-end workflow to analyze and fix a GitHub issue, from reading the issue through opening a PR. Usage: /fix-issue <issue-number>
disable-model-invocation: true
---

Analyze and fix GitHub issue: $ARGUMENTS

Steps:
1. Read the issue: `gh issue view $ARGUMENTS` — understand the reported behavior and expected behavior
2. Reproduce mentally or with a test: write a failing test that demonstrates the bug before touching production code
3. Explore affected code: find the root cause (use a subagent if the codebase is large)
4. Implement the minimal fix — do not refactor unrelated code
5. Confirm the failing test now passes: `[TEST_SINGLE]`
6. Run `[TYPECHECK]` and `[TEST_ALL]` — all must be green
7. Run `[LINT]` — zero warnings
8. Commit: `fix(scope): short description` — imperative mood, under 72 chars
9. Push: `git push -u origin <branch-name>`
10. Open a PR: title under 70 chars; body explains root cause and approach
11. Provide the local checkout commands for the user to test

Do not close the issue automatically. Wait for the user to confirm and ask you to close it.
