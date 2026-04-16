---
name: sentinel-scan
description: >
  Run Sentinel market scans — stock and crypto signal detection using Finnhub and CoinGecko APIs.
  Triggers: 'market scan', 'run sentinel', 'stock scan', 'crypto scan', 'sentinel'.
disable-model-invocation: true
context: fork
allowed-tools: Read, Bash, WebSearch, WebFetch
---
# Sentinel — Market Scanner

Scan stock and crypto markets for actionable signals.

## Data Sources

### Stocks (Finnhub)
- Top gainers/losers of the day
- Unusual volume spikes
- Earnings surprises (beat/miss)
- Insider trading activity
- Analyst upgrades/downgrades

### Crypto (CoinGecko)
- Top movers (24h % change)
- Volume anomalies
- New listings gaining traction
- Fear & Greed index shift
- Trending coins

## Signal Scoring

Score each signal 1-10 based on:
- **Momentum** (3 pts): Price action direction and strength
- **Volume** (2 pts): Above-average volume confirmation
- **Catalyst** (3 pts): News, earnings, or event driver
- **Risk** (2 pts): Inverse — lower risk = higher score

## Output Format

For each signal:
```
📊 [TICKER/COIN] — [Signal Type]
Score: [X/10]
Price: $[current] ([+/-X%] 24h)
Volume: [X]x average
Catalyst: [1-sentence reason]
Risk: [Low | Medium | High]
Action: [Watch | Consider Entry | Strong Signal]
```

## Delivery

1. Scan both stocks and crypto
2. Score all signals
3. Filter to score >= 6
4. Sort by score descending
5. Take top 5 stocks + top 5 crypto
6. Send via iMessage to 3364554699
7. Include disclaimer: "Not financial advice. Do your own research."

## Constraints
- Use free API tiers only (Finnhub free, CoinGecko free)
- Never recommend specific buy/sell actions — only highlight signals
- Flag any signal that contradicts the broader market trend
- Include the Fear & Greed index as context at the top
