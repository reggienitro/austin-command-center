---
name: backlog-manager
description: >
  Manages Notion task databases with strict project routing. Use to create new
  tasks, audit existing ones, or check task status across HububApp,
  article-to-audio, Morning Briefing, and claude-config. Invoke with
  /backlog-manager [action] [project] [details].
disable-model-invocation: true
context: fork
allowed-tools: Read, Grep, Glob, Bash, mcp__notion__query_database, mcp__notion__create_page, mcp__notion__update_page
---
# Backlog Manager

Manage tasks across all active Notion project databases.

## Project Routing Table

**ALWAYS route tasks to the correct database. Never create a task in the wrong project.**

| Project | Notion Collection | Description |
|---------|------------------|-------------|
| HububApp | collection://13b876d5-56a2-4cff-b636-530ed4360d3e | Household management React/Next.js app |
| article-to-audio | collection://32ee1866-9e14-4c4a-b560-74f8573886b6 | Article-to-audio pipeline (news, TTS) |
| Morning Briefing | collection://043c79e6-23f4-4e05-979d-60bcd869d698 | Daily morning briefing automation |
| claude-config | page 3078a76eab8681e7916ac1cfc581ad5c | Claude Code configuration and tooling |

## Routing Rules

1. If the task involves React components, Supabase, or household features → **HububApp**
2. If the task involves RSS feeds, TTS, audio pipelines, or news ingestion → **article-to-audio**
3. If the task involves the briefing format, delivery, or scheduling → **Morning Briefing**
4. If the task involves Claude rules, skills, agents, or config → **claude-config**
5. If ambiguous: ask Austin before creating the task

## Actions

### create — Add a new task

Prompt format: `/backlog-manager create [project] "[task title]" [priority: high|medium|low]`

Before creating:
1. Check if a similar task already exists in the target database (search by title keywords)
2. If a duplicate is found, report it and ask whether to proceed
3. If no duplicate, create with:
   - Title: provided task name
   - Status: Todo
   - Priority: provided (default: medium)
   - Created date: today

### audit — Review and clean up tasks

Prompt format: `/backlog-manager audit [project|all]`

For each target database:
1. Fetch all tasks
2. Flag tasks that are:
   - In "In Progress" for more than 7 days
   - Blocked with no blocker noted
   - Done but not archived
   - Missing priority
3. Print a summary report with recommended actions

### status — Check current task state

Prompt format: `/backlog-manager status [project|all]`

Query the target database(s) and print:

```
PROJECT: [name]
─────────────────────────────
In Progress: [N]
  - [task name] (priority: [P], [N] days old)
Todo: [N]
  - [task name] (priority: [P])
Blocked: [N]
  - [task name] — [blocker note if available]
Done (this week): [N]
```

### move — Update task status

Prompt format: `/backlog-manager move [task ID or name] [new status]`

Valid statuses: Todo, In Progress, Blocked, Done, Cancelled

Always confirm before moving to Done or Cancelled.

## Task Quality Rules

- Titles must be actionable (start with a verb): "Add", "Fix", "Build", "Research", "Refactor"
- Never create vague tasks like "work on X" or "look into Y"
- High priority = must ship this week
- Medium priority = should ship this sprint
- Low priority = nice to have, no deadline
- Add a one-sentence description to any task that isn't self-explanatory
