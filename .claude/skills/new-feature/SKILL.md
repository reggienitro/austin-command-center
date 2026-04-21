---
name: new-feature
description: Scaffold a new feature in this codebase following its conventions. Use when adding a new capability, endpoint, page, or module.
triggers: ["new feature", "add feature", "scaffold"]
---

# new-feature

1. Read the project's CLAUDE.md and at least one similar existing feature for pattern reference.
2. Write the smallest vertical slice (data → logic → presentation/interface).
3. Add a test (match the style of existing tests in this repo).
4. Run the project's test command: `./scripts/validate.sh 2>/dev/null || echo no-validate`.
5. If tests pass, commit with a conventional-commit subject (`feat: <what>`).
6. Never add features outside the asked scope.
