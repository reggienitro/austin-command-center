---
name: test-debug
description: Isolate and fix a failing test in this codebase. Use when `./scripts/validate.sh 2>/dev/null || echo no-validate` fails and the cause isn't immediately obvious.
triggers: ["test fail", "debug test", "fix broken test"]
---

# test-debug

1. Run only the failing test (most runners support a filter flag — check the CLAUDE.md or the project docs).
2. Read the failing assertion + the target module. `git log --oneline -10 <module>` to see recent changes.
3. Fix the smallest thing. Re-run. Confirm.
4. Never `git reset --hard` or `rm -rf`.
5. If the test is legitimately broken vs the code (flaky), fix the test — don't retry-wrap real failures.
