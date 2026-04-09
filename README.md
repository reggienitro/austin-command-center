# austin-command-center

Austin's personal Claude Code plugin — session bootstrapping, project routing, handoff generation, and backlog management.

## Install

```bash
claude plugin add reggienitro/austin-command-center
```

## Skills

### `/load-config` — Session Boot Sequence

Runs at the start of every new session. Loads all rules from `claude-config`, queries Notion for active backlog across all 4 projects, reads the memory index, and prints a status summary including baby countdown.

**When to use:** First thing in every new session.

---

### `/session-handoff` — Handoff Package Generator

Generates a structured handoff package with live Notion data and a ready-to-paste kickoff prompt for the next session. Writes:

- `PROJECT_STATE.md` — current git state, active tasks, session work summary
- `KICKOFF_PROMPT.md` — paste-ready prompt for the next session
- `MEMORY_INDEX.md` — snapshot of the memory index
- `LAST-SESSION-HANDOFF.md` — same kickoff prompt saved to `~/claude-config/docs/`

**When to use:** End of any significant work session, before switching contexts.

---

### `/backlog-manager` — Notion Task Manager

Creates, audits, and checks the status of tasks across all 4 Notion project databases with strict routing rules to ensure tasks land in the correct project.

**Actions:**
- `/backlog-manager create [project] "[title]" [priority]` — add a new task
- `/backlog-manager audit [project|all]` — review and flag stale/broken tasks
- `/backlog-manager status [project|all]` — print current task counts by status
- `/backlog-manager move [task] [status]` — update a task's status

**Projects:** HububApp · article-to-audio · Morning Briefing · claude-config

---

## References

- `skills/load-config/references/notion-structure.md` — full Notion project ID map

## Related

- [claude-config](https://github.com/reggienitro/claude-config) — base rules, agents, and skills
