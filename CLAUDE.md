# Claude Code — Global Instructions

## PR and issue comment formatting

When writing PR descriptions, issue comments, or any GitHub-facing text body, **do not hard-wrap lines**. Write each paragraph as a single continuous line with no embedded newlines. GitHub renders bare newlines as line breaks, which causes mid-sentence breaks in the rendered output. Separate paragraphs with a blank line instead.

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

## GitHub MCP tools — availability and retries

The GitHub MCP server runs with `MCP_CONNECTION_NONBLOCKING=true`, which means the session starts before the server finishes connecting. Tools may not be available immediately. The `gh` CLI and `hub` CLI are **not** available in this environment, so there is no shell fallback.

**At the start of any task that needs GitHub tools**, always call ToolSearch with `"query": "mcp__github"` proactively — before you need a specific tool. This gives the MCP server time to finish connecting and surfaces the tool schemas early.

**If a tool call fails or ToolSearch returns no results:**
1. Wait a moment, then retry ToolSearch once more.
2. If tools are still unavailable after two ToolSearch attempts, tell the user: *"The GitHub MCP server is not responding. Please start a new session and try again."* Do not keep retrying in a loop.

---

## Closing GitHub issues with the MCP tools

Do **not** comment on or close an issue after pushing. There may be many
pushes with their own commit messages — duplicate issue comments are not
needed.

Wait until the user explicitly asks you to close the issue. That means the
user has tested locally, approved the PR, and is ready to wrap up.

When the user asks you to close the issue, first run ToolSearch for `"mcp__github"` to ensure the tools are loaded, then do both steps below in order. If tools remain unavailable after retrying per the instructions above, report failure to the user.

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
