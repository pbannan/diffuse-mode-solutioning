---
name: create-feature
description: Structured workflow for implementing a new feature from spec or issue through to a PR-ready branch. Usage: /create-feature <description or issue-number>
disable-model-invocation: true
---

Implement feature: $ARGUMENTS

Steps:
1. Read the spec or issue first: `gh issue view [issue]` if an issue number was given
2. Explore related existing code — understand the patterns in use before writing new code
3. Plan: list every file you will create or modify before touching anything; share the plan
4. Implement — one logical commit per meaningful unit of work; keep commits small
5. Write tests covering the new behavior, edge cases, and error paths
6. Run `[TYPECHECK]` — zero errors
7. Run `[TEST_ALL]` — full suite green
8. Run `[LINT]` — zero warnings
9. Push: `git push -u origin <branch-name>`
10. Open a PR: title under 70 chars; body explains what was built and why
11. Provide the local checkout commands for the user to test

Do not:
- Add features or options beyond what was specified
- Refactor existing code unless it directly blocks the implementation
- Skip the test step
- Push to `main` directly
