---
description: Structured review of current branch vs the default branch.
---

# /review $ARGUMENTS

1. Resolve default branch: `git symbolic-ref refs/remotes/origin/HEAD | sed 's|.*/||'`.
2. `gtimeout 5 git diff origin/<default>...HEAD --stat` — scope.
3. `gtimeout 5 git diff origin/<default>...HEAD` — full diff.
4. For each file, assess: correctness, security, style (per `~/.claude/rules/`), test coverage, risk.
5. Output: **Must fix**, **Should fix**, **Nit**, **Good**. Stop on any MUST-FIX and surface to Austin.
