---
name: rg-arcade-reader
description: Use when Codex needs RaidGuild Arcade leaderboard scores or daily activity summaries for Brood Tapper or Hack Thy Sack.
metadata:
  gateway-capabilities:
    - arcade.brood.scores.read
    - arcade.brood.days.read
    - arcade.hack-thy-sack.scores.read
    - arcade.hack-thy-sack.days.read
---

# RaidGuild Arcade Reader

Use the assigned Prism Gateway capabilities for read-only RaidGuild Arcade
questions. Do not read `ARCADE_AGENT_API_KEY`, call game APIs directly, or fall
back to runtime credentials.

Invoke a capability by posting to `$PRISM_RUNTIME_CAPABILITY_URL` with
`x-runtime-capability-token: $PRISM_RUNTIME_CAPABILITY_TOKEN`.

## Capabilities

Leaderboard scores:

- `arcade.brood.scores.read`
- `arcade.hack-thy-sack.scores.read`

Use one of these inputs:

```json
{ "scope": "all-time", "limit": 10 }
```

```json
{ "scope": "day", "date": "YYYY-MM-DD", "tz": "America/Denver", "limit": 10 }
```

Daily activity summaries:

- `arcade.brood.days.read`
- `arcade.hack-thy-sack.days.read`

Daily summary input requires both date and timezone:

```json
{ "date": "YYYY-MM-DD", "tz": "America/Denver" }
```

## Output

Expose only public leaderboard fields such as handle, rank, score, duration,
played time, and public game-specific statistics. Do not expose profile IDs,
player IDs, game IDs, launch-token claims, raw internal payloads, Gateway
tokens, or provider credentials.

For a multi-game request, invoke the matching capability for each game and
clearly identify each result. Use `rg-content-strategy`, `rg-brand-voice`, and
`rg-public-output-safety` when turning results into a public report.
