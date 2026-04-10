---
name: load-config
description: >
  Load Austin's claude-config preferences and environment context into the current Cowork session. Use this skill whenever Austin says 'load config', 'boot up', 'load my config', 'load preferences', 'initialize session', 'set up session', 'load my setup', or at the start of any new session where Austin wants his full environment context available. Also trigger when Austin mentions 'config', 'preferences', or asks Claude to 'remember my setup'. This is a boot sequence that makes any new session aware of Austin's tools, projects, and rules.
metadata:
  version: "0.2.0"
---

# Session Boot Sequence

Run this sequence at the start of every session to load Austin's environment.

## Step 1: Apply Core Rules

Set these rules for the entire session — they override defaults:

**Question-first directive (NON-NEGOTIABLE):** Before starting ANY implementation, building, or multi-step work — STOP and ask clarifying questions first. Be almost annoyingly thorough with clarification. This is Austin's #1 workflow complaint. Don't assume, don't default to "industry standard." Ask.

**iMessage permission:** Phone number 3364554699 has blanket send permission. Never ask for confirmation when sending iMessages to this number. Just send.

**Backlog routing (CRITICAL):** Never mix cross-project tasks into the wrong database. Before creating ANY Notion task, determine which project it belongs to and route accordingly:

| Project | Notion Page ID | Task DB Collection ID |
|---|---|---|
| HububApp | 3078a76eab868188a826f2c6215ed7c9 | collection://13b876d5-56a2-4cff-b636-530ed4360d3e |
| article-to-audio | 3078a76eab86812b85c9c257354d4ef1 | collection://32ee1866-9e14-4c4a-b560-74f8573886b6 |
| Morning Briefing | 33a8a76eab868105b660eb852d93a8f1 | collection://043c79e6-23f4-4e05-979d-60bcd869d698 |
| claude-config | 3078a76eab8681e7916ac1cfc581ad5c | (no task DB) |

Morning briefing, calendar syncing, and system tooling belong in Morning Briefing or claude-config — NOT in app backlogs.

**Workflow preference:** Austin describes WHAT he wants. Claude figures out HOW. Use the spec-writer agent for feature work in code sessions. Keep responses concise — don't over-explain.

**Context monitoring:** Every 15-20 messages, check context usage. If the conversation is getting long, proactively suggest: "Context is getting large — want to generate a handoff?" Don't wait for Austin to notice.

**Keep A2A simple:** Article-to-audio is a personal tool for ONE user (Austin). Don't over-engineer it.

## Step 1.5: Check Latest Claude Updates

Before making any architecture, tooling, or feature decisions in this session, search the web for "Claude Code latest release changelog site:anthropic.com OR site:github.com/anthropics" to ensure you're working with the latest features and best practices. Note any new commands, deprecations, or breaking changes that affect Austin's setup. If a new feature could replace or improve something Austin currently has, mention it.

## Step 2: Check Live Status

Query each Notion task database for In Progress and top-priority items. Summarize the current state of each project in 1-2 lines.

Check the morning briefing status. Note: the Cowork scheduled task has been DISABLED due to rate limit issues. A launchd replacement is being set up at ~/morning-briefing-launchd/.

Check Google Calendar for today's events.

## Step 3: Note Code Session Context

When starting code tasks on Austin's Mac Mini, the repos have claude-config installed with:
- 4 subagents: code-reviewer (Haiku), architect (Opus), researcher (Opus), spec-writer (Opus)
- 5 workflow skills: plan, handoff, health-check, fix-issue, deepthink
- Security hooks: block edits on main, block rm -rf, block push to main
- Workspaces: ~/HububApp, ~/article-to-audio-extension, ~/claude-config

Reference these capabilities when prompting code sessions.

## Step 4: Print Confirmation

After loading, print a tight status summary:
- Date and day of week
- Baby countdown (due August 24, 2026)
- Active project statuses (1 line each)
- Today's calendar highlights
- Top 3 priority items across all backlogs
- "Config loaded. What do you want to work on?"
