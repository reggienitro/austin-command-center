---
name: session-handoff
description: >
  Generate a handoff zip with live Notion data, memory snapshot, and kickoff prompt for the next session.
  Triggers: 'session handoff', 'handoff', 'pack up session', 'transfer context', 'generate handoff'.
disable-model-invocation: true
context: fork
allowed-tools: Read, Grep, Glob, Bash
---
# Session Handoff Generator

Generate a complete handoff package for continuing work in a new session.

## Step 1: Collect Session State

Run these commands to capture current state:
```bash
pwd
git branch --show-current 2>/dev/null || echo "no git repo"
git status --short 2>/dev/null || echo "no git repo"
git log --oneline -5 2>/dev/null || echo "no git repo"
date
```

## Step 2: Query Live Notion Data

Query all 3 active task databases for current state:

| Project | Notion Collection |
|---------|------------------|
| HububApp | collection://13b876d5-56a2-4cff-b636-530ed4360d3e |
| article-to-audio | collection://32ee1866-9e14-4c4a-b560-74f8573886b6 |
| Morning Briefing | collection://043c79e6-23f4-4e05-979d-60bcd869d698 |

For each, fetch all tasks with status not "Done" or "Cancelled".

## Step 3: Read Memory Index

Read all files referenced in `~/.claude/projects/-Users-austinettefagh/memory/MEMORY.md`.

## Step 4: Generate PROJECT_STATE.md

Write to `~/claude-config/docs/handoff/PROJECT_STATE.md`:

```markdown
# Project State — [DATE]

## Git Status
- Repo: [current repo]
- Branch: [branch name]
- Uncommitted changes: [git status output]
- Recent commits: [last 5 commits]

## Active Notion Tasks

### HububApp
[list of non-done tasks with status and priority]

### article-to-audio
[list of non-done tasks with status and priority]

### Morning Briefing
[list of non-done tasks with status and priority]

## Session Work
- Completed this session: [bullet list]
- In progress: [bullet list]
- Blocked: [bullet list]

## Key Decisions Made
[Any architectural or design decisions from this session]

## Files Modified
[List of files changed this session]
```

## Step 5: Generate KICKOFF_PROMPT.md

Write to `~/claude-config/docs/handoff/KICKOFF_PROMPT.md`:

```markdown
I'm Austin Ettefagh (@reggienitro). Continuing from a prior session on [DATE].

Check ~/.claude/projects/-Users-austinettefagh/memory/MEMORY.md for full context.

## What was accomplished this session
[bullet list of completed work]

## What's in progress / next up
[bullet list of remaining items with current state]

## Key decisions made
[any architectural or design decisions from this session]

## Files modified this session
[list of files changed]

Start by running /load-config to initialize context, then continue with [NEXT PRIORITY].
```

## Step 6: Generate MEMORY_INDEX.md

Write to `~/claude-config/docs/handoff/MEMORY_INDEX.md`:

Copy the full contents of `~/.claude/projects/-Users-austinettefagh/memory/MEMORY.md`
and all referenced memory files into the handoff directory.

## Step 7: Save and Confirm

Also write the kickoff prompt to `~/claude-config/docs/LAST-SESSION-HANDOFF.md`
(overwrites previous).

Print confirmation:
```
╔══════════════════════════════════════════════════════════════╗
║  HANDOFF PACKAGE GENERATED                                   ║
╚══════════════════════════════════════════════════════════════╝

Files written:
  ~/claude-config/docs/handoff/PROJECT_STATE.md
  ~/claude-config/docs/handoff/KICKOFF_PROMPT.md
  ~/claude-config/docs/handoff/MEMORY_INDEX.md
  ~/claude-config/docs/LAST-SESSION-HANDOFF.md

Paste KICKOFF_PROMPT.md into your next session to resume.
```
