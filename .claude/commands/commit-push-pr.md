---
description: Stage, commit, push current branch, open PR.
---

# /commit-push-pr $ARGUMENTS

1. `gtimeout 10 git status` — review changes.
2. Draft conventional-commit subject (feat/fix/chore/docs/refactor). Use $ARGUMENTS if given.
3. Stage ONLY files you edited (never `git add -A` — leaks WIP/secrets).
4. Commit with Co-Authored-By trailer.
5. **iMessage Austin at 3364554699** with PR summary + branch name. Wait for reply.
6. `gtimeout 30 git push -u origin <branch>`.
7. Open PR via the `github` MCP server (NOT `gh` CLI — it hangs).
8. Return PR URL.

Abort if current branch is main/master.
