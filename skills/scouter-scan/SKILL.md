---
name: scouter-scan
description: >
  Run Scouter opportunity scans — freelance gigs, micro-SaaS ideas, and trending markets matching Austin's skills.
  Triggers: 'scan opportunities', 'run scouter', 'find gigs', 'opportunity scan', 'scouter'.
disable-model-invocation: true
context: fork
allowed-tools: Read, Bash, WebSearch, WebFetch
---
# Scouter — Opportunity Scanner

Scan the web for realistic money-making opportunities matching Austin's skill stack.

## Skill Stack Filter

Only surface opportunities matching these skills:
- AI automation (Claude Code, MCP servers, agent workflows)
- Chrome extensions / browser tooling
- React / Next.js / TypeScript / Supabase
- Salesforce / nCino consulting
- Content creation (AI-assisted writing, newsletters)

## Scan Categories

### 1. Freelance Gigs
Search these sources for relevant postings:
- Upwork: AI automation, Claude, Salesforce
- Toptal / Gun.io: senior-level React/Next.js
- r/forhire, r/slavelabour: quick automation gigs
- Freelancer.com: AI/ML category

### 2. Micro-SaaS Ideas
Search for pain points and opportunities:
- IndieHackers: trending ideas and revenue reports
- ProductHunt: gaps in recently launched tools
- r/SaaS, r/microsaas: unmet needs

### 3. Trending Markets
Search for emerging demand signals:
- AI tool directories: what categories are growing
- Chrome Web Store: extension gaps
- Supabase showcase: what's getting traction

### 4. Affiliate / Content
- AI tool affiliate programs
- Newsletter sponsorship opportunities
- Course/tutorial demand signals

## Output Format

For each opportunity found:
```
🎯 [OPPORTUNITY TITLE]
Category: [Freelance | SaaS | Market | Content]
Potential: [$/timeframe estimate]
Effort: [Low | Medium | High]
Match: [which skills apply]
Link: [URL]
Why: [1-sentence reasoning]
```

## Delivery

1. Score each opportunity 1-10 based on: skill match, effort-to-reward ratio, time-to-revenue
2. Sort by score descending
3. Take top 5
4. Send results via iMessage to 3364554699
5. Format as a tight summary — no fluff

## Notes
- Skip anything requiring >$500 upfront investment
- Skip anything requiring a team
- Prefer opportunities with revenue potential within 30 days
- Flag any that could be automated with Claude Code
