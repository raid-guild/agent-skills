# Arcade Agent APIs

Use this as Portal-adjacent read-only API reference for Portal Arcade games.

This is not a standalone publishing/reporting skill. Recurring leaderboard summaries should be workflow recipes that compose Portal data access, content strategy, public safety, and publishing ops.

## Scope

Read-only gameplay and leaderboard questions across configured arcade games.

Do not:

- submit scores
- modify game data
- expose internal identifiers
- expose bearer tokens

## Environment

- `ARCADE_AGENT_API_KEY`: shared bearer token for `/api/agent/*` routes.
- `BROOD_TAPPER_BASE_URL`: Brood Tapper base URL.
- `HACK_THY_SACK_BASE_URL`: Hack Thy Sack base URL.

If config is missing, report missing variable names only.

## Game Registry

- Brood Tapper: `BROOD_TAPPER_BASE_URL`, route prefix `/api/agent`, score extras may include `glasses`.
- Hack Thy Sack: `HACK_THY_SACK_BASE_URL`, route prefix `/api/agent`, score fields include `durationMs`.

Future games should provide their own `*_BASE_URL`, use `ARCADE_AGENT_API_KEY`, and confirm the same `/api/agent/scores` and `/api/agent/days` contract.

## Endpoints

Authenticate with:

```text
Authorization: Bearer $ARCADE_AGENT_API_KEY
```

Read-only endpoints:

- `GET /api/agent/scores?scope=all-time&limit=10`
- `GET /api/agent/scores?scope=day&date=YYYY-MM-DD&tz=America/Denver&limit=10`
- `GET /api/agent/days?date=YYYY-MM-DD&tz=America/Denver`

## Data Exposure

Expose only:

- handle
- rank
- score
- duration
- played time
- public game-specific stats

Do not expose:

- profile ids
- player ids
- game ids
- launch token claims
- raw internal payloads

## Reporting Workflows

For public or Discord reports, compose:

1. Portal arcade API read
2. `rg-content-strategy` for summary shape
3. `rg-brand-voice` if public-facing
4. `rg-public-output-safety`
5. `rg-publishing-ops`
