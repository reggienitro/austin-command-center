# austin-command-center — Project Constitution

## Overview
Austin's personal Claude Code plugin. Provides session bootstrapping (`/load-config`), handoff generation (`/session-handoff`), cross-project backlog management (`/backlog-manager`), opportunity scanning (`/scouter-scan`), market signal detection (`/sentinel-scan`), and Notion task routing (`/notion-route`). Installed via `claude plugin add` and consumed by both Claude Code CLI sessions and Cowork desktop sessions. This is the operational glue that keeps multi-project work consistent across sessions.

## Architecture

```
austin-command-center/
  ├── .claude-plugin/
  │   └── plugin.json      ← Plugin manifest (name, version, description, keywords)
  ├── skills/
  │   ├── load-config/
  │   │   └── SKILL.md     ← Session boot sequence: rules, Notion status, calendar check
  │   ├── session-handoff/
  │   │   └── SKILL.md     ← Generates handoff package with live Notion data + kickoff prompt
  │   ├── backlog-manager/
  │   │   └── SKILL.md     ← CRUD for Notion task databases with strict project routing
  │   ├── scouter-scan/
  │   │   └── SKILL.md     ← Freelance gig, micro-SaaS, and trending market scanner
  │   ├── sentinel-scan/
  │   │   └── SKILL.md     ← Stock and crypto signal detection (Finnhub + CoinGecko)
  │   └── notion-route/
  │       └── SKILL.md     ← Notion task creation with strict project-to-DB routing
  └── README.md            ← Usage documentation
```

**Tech stack:** Pure Markdown skill definitions. No runtime code — skills are prompts that orchestrate Claude's tool use (Notion MCP, Bash, file tools).

## Key Files

| File | Purpose |
|---|---|
| `.claude-plugin/plugin.json` | Plugin manifest: name, version, author, repository URL |
| `skills/load-config/SKILL.md` | **Session boot:** loads rules, checks Notion task status across 4 projects, reads calendar, prints confirmation |
| `skills/session-handoff/SKILL.md` | **Handoff generator:** captures git state, queries all 3 Notion task DBs, reads memory index, writes PROJECT_STATE.md + KICKOFF_PROMPT.md |
| `skills/backlog-manager/SKILL.md` | **Task CRUD:** create tasks with strict project routing, audit stale/broken tasks, check status across all databases |
| `skills/scouter-scan/SKILL.md` | **Opportunity scanner:** freelance gigs, micro-SaaS ideas, trending markets matching Austin's skills; delivers top 5 via iMessage |
| `skills/sentinel-scan/SKILL.md` | **Market scanner:** stock and crypto signal detection using Finnhub + CoinGecko; scores signals 1-10, delivers top picks via iMessage |
| `skills/notion-route/SKILL.md` | **Task router:** creates Notion tasks with strict project-to-database routing; enforces title conventions and deduplication |
| `README.md` | Usage docs for all 6 skills |

## Notion Project Routing (CRITICAL)

The backlog manager enforces strict routing — tasks must go to the correct Notion database:

| Project | Notion Collection ID | What goes here |
|---|---|---|
| HububApp | `collection://13b876d5-56a2-4cff-b636-530ed4360d3e` | React components, Supabase, household features |
| article-to-audio | `collection://32ee1866-9e14-4c4a-b560-74f8573886b6` | RSS feeds, TTS, audio pipelines, news ingestion |
| Morning Briefing | `collection://043c79e6-23f4-4e05-979d-60bcd869d698` | Briefing format, delivery, scheduling |
| claude-config | page `3078a76eab8681e7916ac1cfc581ad5c` | Claude rules, skills, agents, config |
| Scheduled Task Runs | `collection://49af2959-04f5-4d6f-befc-80cdf1f00d55` | Task run logging, observability |

## Install & Use

```bash
# Install plugin
claude plugin add reggienitro/austin-command-center

# Use in any Claude Code session:
/load-config                              # Boot sequence
/session-handoff                          # Generate handoff package
/backlog-manager create hubub "Add dark mode" high
/backlog-manager audit all
```

## Skill Details

### `/load-config` — Session Boot Sequence
1. Apply core rules (question-first directive, iMessage permission, backlog routing)
2. Check latest Claude Code updates (web search)
3. Query Notion for In Progress tasks across all projects
4. Check Google Calendar for today's events
5. Note available subagents and skills from claude-config
6. Print status confirmation

### `/session-handoff` — Handoff Package
1. Capture git state (branch, status, recent commits)
2. Query all 3 Notion task databases for non-done tasks
3. Read memory index
4. Write: `PROJECT_STATE.md`, `KICKOFF_PROMPT.md`, `MEMORY_INDEX.md`
5. Save kickoff prompt to `~/claude-config/docs/LAST-SESSION-HANDOFF.md`

### `/backlog-manager` — Task Management
- `create [project] "[title]" [priority]` — checks for duplicates, then creates
- `audit [project|all]` — flags stale In Progress, missing priority, done-but-not-archived

### `/scouter-scan` — Opportunity Scanner
1. Scan freelance boards (Upwork, Toptal, r/forhire), micro-SaaS communities (IndieHackers, ProductHunt), and trending markets
2. Filter for Austin's skill stack (AI automation, React/Next.js, Salesforce, Chrome extensions)
3. Score opportunities 1-10 by skill match, effort-to-reward, time-to-revenue
4. Deliver top 5 via iMessage

### `/sentinel-scan` — Market Scanner
1. Pull stock signals via Finnhub (gainers/losers, volume spikes, earnings surprises, insider activity)
2. Pull crypto signals via CoinGecko (top movers, volume anomalies, trending coins, Fear & Greed index)
3. Score signals 1-10 across momentum, volume, catalyst, risk
4. Deliver top 5 stocks + top 5 crypto via iMessage

### `/notion-route` — Task Router
1. Parse task description for project keywords
2. Route to correct Notion database using hardcoded project-to-DB mapping
3. Enforce: verb-first titles, duplicate check, priority assignment, default status = Todo
4. Special handling: claude-config (sub-pages, no task DB), cross-project routing, Scouter/Sentinel → Morning Briefing

## Workflow Rules
- Direct pushes to main (personal plugin, single developer)
- Use `timeout 15` on git push/pull
- When modifying skills, test in a real session before committing
- Skill files use YAML frontmatter: `name`, `description`, `disable-model-invocation`, `context`, `allowed-tools`

## Common Pitfalls
- **Notion collection IDs are hardcoded in skills** — if Notion databases are restructured, update the routing table in ALL skills
- **Skills reference `~/.claude/` paths** — these are symlinks from claude-config; if symlinks break, skills fail silently
- **Morning Briefing scheduled task is DISABLED** — rate limit issues; a launchd replacement is being set up
- **Memory index path** — `~/.claude/projects/-Users-austinettefagh/memory/MEMORY.md`

## Related Projects
- **claude-config** (`~/claude-config`) — Provides the rules, agents, and config that load-config activates
- **All project repos** — backlog-manager routes tasks to HububApp, A2A, Morning Briefing, claude-config Notion boards
