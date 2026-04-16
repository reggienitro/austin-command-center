---
name: notion-route
description: >
  Create Notion tasks with correct backlog routing across all project databases. Enforces strict project-to-DB mapping.
  Triggers: 'add task', 'create backlog item', 'add to notion', 'backlog', 'new task', 'notion task'.
disable-model-invocation: true
context: fork
allowed-tools: Read, Bash
---
# Notion Task Router

Create tasks in the correct Notion database. **Never create a task in the wrong project.**

## Routing Table

| Project | Page ID | Task DB Collection ID | Route When |
|---|---|---|---|
| HububApp | 3078a76eab868188a826f2c6215ed7c9 | collection://13b876d5-56a2-4cff-b636-530ed4360d3e | React components, Supabase, household features, UI/UX |
| article-to-audio | 3078a76eab86812b85c9c257354d4ef1 | collection://32ee1866-9e14-4c4a-b560-74f8573886b6 | RSS feeds, TTS, audio pipelines, news ingestion, podcasts |
| Morning Briefing | 33a8a76eab868105b660eb852d93a8f1 | collection://043c79e6-23f4-4e05-979d-60bcd869d698 | Briefing format, delivery, scheduling, iMessage automation |
| claude-config | 3078a76eab8681e7916ac1cfc581ad5c | (page only — no task DB) | Claude rules, skills, agents, MCP config, plugin dev |
| Scheduled Task Runs | 2628a76eab8680718b80e401bd4a46c1 | collection://49af2959-04f5-4d6f-befc-80cdf1f00d55 | Task run logging, observability |

## Routing Rules

1. Parse the task description for project keywords
2. Match against the "Route When" column
3. If ambiguous → **ask Austin before creating**
4. If the task spans multiple projects → create in the primary project, note cross-project dependency

## Task Creation Checklist

Before creating any task:
- [ ] Title starts with a verb (Add, Fix, Build, Research, Refactor, Implement)
- [ ] Correct database selected from routing table
- [ ] Check for duplicate (search by title keywords in target DB)
- [ ] Priority assigned: High (ship this week), Medium (this sprint), Low (no deadline)
- [ ] Status set to: Todo

## Task Properties

When creating a page in a task database, set:
- **Title**: Actionable task name
- **Status**: Todo (default)
- **Priority**: As specified or Medium
- **Description**: 1-sentence context if not self-explanatory

## Special Cases

- **claude-config has no task DB** — log tasks as sub-pages under page 3078a76eab8681e7916ac1cfc581ad5c
- **Cross-project work** (e.g., "add TTS to morning briefing") → route to the project that owns the feature being built (article-to-audio), not the consumer (Morning Briefing)
- **Meta-tasks** about the command center plugin itself → claude-config
- **Scouter/Sentinel tasks** → Morning Briefing (they're part of the briefing pipeline)

## Anti-Patterns

- ❌ Vague titles: "work on X", "look into Y", "stuff for Z"
- ❌ Missing priority on high-urgency items
- ❌ Creating in the wrong DB because the task mentions multiple projects
- ❌ Duplicating a task that already exists
