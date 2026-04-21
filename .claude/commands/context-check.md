---
description: Report session context usage and recommend compaction focus.
---

# /context-check $ARGUMENTS

1. Check current context % (autocompact override: 70% via env var).
2. List 3 most context-heavy sources (long tool results, full-file Reads, verbose subagent reports).
3. Recommend:
   - <50%: stay.
   - 50–70%: `/compact "focus on <current task>"`.
   - 70%+: trigger handoff per `~/.claude/rules/session-health.md`; save to `~/claude-config/docs/LAST-SESSION-HANDOFF.md`.
4. If $ARGUMENTS contains "compact", run `/compact` with the focus hint.
