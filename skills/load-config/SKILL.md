---
name: load-config
description: >
  Session boot sequence for Austin's development environment. Loads rules,
  queries Notion for active backlog across all projects, and prints a status
  summary including baby countdown. Invoke at the start of every new session
  with /load-config.
disable-model-invocation: true
context: fork
allowed-tools: Read, Grep, Glob, Bash, mcp__notion__query_database
---
# Session Boot Sequence

Run the following steps in order to initialize the session.

## Step 1: Load Rules

Read the following files to load active conventions:
- `~/claude-config/CLAUDE.md`
- `~/claude-config/core/CLAUDE-CORE.md`
- `~/claude-config/.claude/rules/coding-style.md`
- `~/claude-config/.claude/rules/git-workflow.md`
- `~/claude-config/.claude/rules/security.md`
- `~/claude-config/.claude/rules/session-health.md`
- `~/claude-config/.claude/rules/web-conventions.md`
- `~/claude-config/.claude/rules/database-conventions.md`

## Step 2: Query Notion Backlog

Query all 4 project task databases for items with status = "In Progress" or "Todo":

| Project | Notion Collection |
|---------|------------------|
| HububApp | collection://13b876d5-56a2-4cff-b636-530ed4360d3e |
| article-to-audio | collection://32ee1866-9e14-4c4a-b560-74f8573886b6 |
| Morning Briefing | collection://043c79e6-23f4-4e05-979d-60bcd869d698 |
| claude-config | page 3078a76eab8681e7916ac1cfc581ad5c |

For each database, fetch:
- Task name
- Status
- Priority
- Assignee (if set)
- Due date (if set)

## Step 3: Load Memory

Read `~/.claude/projects/-Users-austinettefagh/memory/MEMORY.md` and surface any
entries flagged as active or relevant to today's date.

## Step 4: Print Status Summary

Output the following status block:

```
╔══════════════════════════════════════════════════════════════╗
║  AUSTIN COMMAND CENTER — SESSION INITIALIZED                 ║
╚══════════════════════════════════════════════════════════════╝

📅 Date: [today's date]
👶 Baby countdown: [N] days until Aug 24, 2026

📋 ACTIVE BACKLOG
─────────────────
HububApp:         [N] tasks ([N] in progress, [N] todo)
article-to-audio: [N] tasks ([N] in progress, [N] todo)
Morning Briefing: [N] tasks ([N] in progress, [N] todo)
claude-config:    [N] tasks ([N] in progress, [N] todo)

🔧 SESSION CONTEXT
──────────────────
Subagents available: 4 (code-reviewer, architect, researcher, spec-writer)
Skills available:    5 (load-config, session-handoff, backlog-manager, handoff, health-check)
Rules loaded:        8

📱 PERMISSIONS
──────────────
iMessage: blanket permission granted for 3364554699
```

## Workflow Preferences

- Prefer parallel subagent execution for independent research tasks
- Always check Notion backlog before starting new work — don't duplicate tasks
- Commit to feature branches only; never push directly to main
- Use conventional commits: feat:, fix:, chore:, docs:, refactor:
- Surface blockers immediately rather than working around them silently

## Code Session Defaults

**4 subagents available:**
1. `code-reviewer` — runs after any significant code change
2. `architect` — use when planning new features or major refactors
3. `researcher` — use before installing dependencies or evaluating tools
4. `spec-writer` — use before writing code for new features

**5 skills available:**
1. `/load-config` — this skill; run at session start
2. `/session-handoff` — generate handoff zip at session end
3. `/backlog-manager` — create, audit, or check Notion tasks
4. `/handoff` — quick in-session handoff doc (no zip)
5. `/health-check` — validate environment and MCP connectivity
