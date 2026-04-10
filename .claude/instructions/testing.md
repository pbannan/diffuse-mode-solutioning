# Testing

## Strategy

| Level | Scope | When to write |
|-------|-------|---------------|
| Unit | Pure functions, utilities, isolated components | Always |
| Integration | API routes, DB operations, service layer | When touching DB or external services |
| E2E | Critical user flows (login, checkout, etc.) | Sparingly — only for flows that would be catastrophic to break |

Prefer unit tests. Integration tests are slower but necessary for paths that touch the database. E2E tests are expensive — add them only when a unit + integration combination cannot catch the failure.

## Commands

```bash
[TEST_SINGLE]     # run one test by name (use during development)
[TEST_ALL]        # run full suite (required before committing)
[TEST_COVERAGE]   # coverage report (review periodically, not per-commit)
[E2E]             # end-to-end tests (slow; run before releasing)
```

## File Conventions

- **Unit / integration**: co-located with source — `utils/format.ts` → `utils/format.test.ts`
- **E2E**: `e2e/[flow-name].spec.ts`
- **Fixtures / factories**: `tests/factories/[entity].ts`
- **Shared mocks**: `tests/mocks/[service].ts`

## What to Test

**Always test**:
- Boundary conditions: empty arrays, null/undefined, zero, max values
- Error paths: what happens when the DB query fails, external API is down
- Business logic that isn't obvious from reading the code
- Any bug that is fixed — write the failing test first, then fix

**Skip testing**:
- Third-party library internals (trust the library)
- Trivial getters/setters with no logic
- Presentation-only components (snapshot tests add noise without value)
- Things that are already tested by framework infrastructure

## Test Quality

- One assertion focus per test — use multiple tests instead of one mega-test
- Test names describe the scenario: `"returns null when user is not found"`
- Test behavior, not implementation — internals can change without breaking behavior
- No shared mutable state between tests (`beforeEach` should fully reset)
- Async tests: always `await`, and always test the rejection/error case too
- Prefer real implementations over mocks where the real thing is fast enough

## Before Marking a Task Complete

Run all of these; all must be green with zero errors:

```bash
[TEST_SINGLE]   # confirm the specific test(s) for the changed code pass
[TYPECHECK]     # zero type errors
[LINT]          # zero lint warnings
[TEST_ALL]      # full suite green
```
