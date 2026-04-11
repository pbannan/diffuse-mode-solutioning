# Git Workflow

## Branch Naming

`type/short-description` — kebab-case, be specific enough to identify the work.

```
feat/add-google-oauth
fix/token-refresh-infinite-loop
refactor/extract-auth-middleware
docs/update-api-reference
chore/upgrade-prisma-v5
test/add-user-service-coverage
```

## Development Flow

1. Branch from `main` — never push directly to `main`
2. Implement changes — commit small and often
3. Before pushing: run `[TYPECHECK]` and `[TEST_ALL]`; fix all failures
4. Push with `-u`: `git push -u origin <branch-name>`
5. Open a PR against `main`; link the issue with `Closes #[number]`

## After Pushing to a Branch

At the end of every session where you've pushed commits, provide these copy-paste commands so the user can test locally. Replace `<branch-name>` with the actual branch name:

```bash
git fetch origin
git checkout <branch-name>
git pull origin <branch-name>
```

Always include this block (with the real branch name substituted) in your final response before signing off.

## PR Quality

- **Title**: `type(scope): description` under 70 characters
- **Body**: explain *why* the change was made, not just *what* changed (the diff shows what)
- **No hard-wrapped lines** — write each paragraph as a single continuous line; GitHub renders bare newlines as visible line breaks
- Reference the issue: `Closes #[number]`

## Closing Issues

Only close an issue when the user explicitly asks (they have tested locally and approved the PR).

When closing:
1. **Comment** with a summary of the root cause and the changes made to fix it
2. **Close** the issue with `state: closed`, `state_reason: completed`

Do not comment on or close issues automatically after pushing — there may be multiple pushes; duplicate comments are unhelpful.

## Commit Hygiene

- One logical change per commit
- Commit messages: `type(scope): description` — see conventions.md
- Never commit: `.env`, secrets, credentials, build artifacts, `node_modules`
- Never skip hooks: `--no-verify` is not allowed
- Never force-push to shared branches (`main`, `staging`, open PRs)
- Resolve merge conflicts rather than discarding changes
