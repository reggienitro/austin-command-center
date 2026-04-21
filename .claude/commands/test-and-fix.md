---
description: Run project tests, diagnose failures, fix, re-run until green.
---

# /test-and-fix $ARGUMENTS

1. `./scripts/validate.sh 2>/dev/null || echo no-validate 2>&1 | tee /tmp/test.log`
2. If exit 0, report green and stop.
3. Otherwise diagnose each failure from the log. Fix one at a time; re-run; confirm.
4. Never `rm -rf` or `git reset --hard` in the course of fixing.
5. Loop until green or until you hit a failure that needs Austin's decision; then stop and report.
