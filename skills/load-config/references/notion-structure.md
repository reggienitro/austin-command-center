# Notion Project Structure

Full ID map for Austin's active Notion workspaces and task databases.

## Task Databases

| Project | Type | ID |
|---------|------|----|
| HububApp | collection | 13b876d5-56a2-4cff-b636-530ed4360d3e |
| article-to-audio | collection | 32ee1866-9e14-4c4a-b560-74f8573886b6 |
| Morning Briefing | collection | 043c79e6-23f4-4e05-979d-60bcd869d698 |
| claude-config | page | 3078a76eab8681e7916ac1cfc581ad5c |

## Collection URLs

```
HububApp:         collection://13b876d5-56a2-4cff-b636-530ed4360d3e
article-to-audio: collection://32ee1866-9e14-4c4a-b560-74f8573886b6
Morning Briefing: collection://043c79e6-23f4-4e05-979d-60bcd869d698
claude-config:    (page, not collection — query via page ID)
```

## Project Descriptions

### HububApp
React/Next.js household management application. Tracks chores, bills, shared
tasks, and household members. Deployed on Vercel, database on Supabase.

### article-to-audio
Pipeline that ingests news articles from RSS/web sources, summarizes them, and
converts to audio using TTS. Powers Austin's Morning Briefing delivery.

### Morning Briefing
Daily automated briefing assembled from article-to-audio output. Covers AI news,
dev topics, and personal priorities. Delivered on a schedule.

### claude-config
Austin's Claude Code configuration repo — rules, agents, skills, and hooks.
Published at github.com/reggienitro/claude-config.

## Notes

- Collection IDs are used with the Notion MCP's `query_database` tool
- The claude-config entry is a Notion page (not a database collection) — use
  `get_page` or navigate children to find tasks
- IDs are stable and do not change unless the workspace is restructured
