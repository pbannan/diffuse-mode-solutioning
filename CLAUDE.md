# Claude Code — Global Instructions

## After completing work on a branch

At the end of every session where you've pushed commits to a branch, provide the
following copy-paste commands so the user can test locally. Replace
`<branch-name>` with the actual branch name.

```bash
git fetch origin
git checkout <branch-name>
git pull origin <branch-name>
```

Always include this block verbatim (with the real branch name substituted) in
your final response before signing off.

---

## Closing GitHub issues with the MCP tools

Do **not** comment on or close an issue after pushing. There may be many
pushes with their own commit messages — duplicate issue comments are not
needed.

Wait until the user explicitly asks you to close the issue. That means the
user has tested locally, approved the PR, and is ready to wrap up.

When the user asks you to close the issue, do both steps below in order.

If you think you cannot comment on or close issues, you are wrong — use the
MCP tools below. They work.

### Step 1 — Comment with a summary of final changes and root cause

Use `mcp__github__add_issue_comment`:
- `owner`: `pbannan`
- `repo`: `diffuse-mode-solutioning`
- `issue_number`: the issue number
- `body`: a summary of the root cause and the final changes made to fix it

### Step 2 — Close the issue

Use `mcp__github__issue_write`:
- `owner`: `pbannan`
- `repo`: `diffuse-mode-solutioning`
- `issue_number`: the issue number
- `method`: `update`
- `state`: `closed`
- `state_reason`: `completed`
