---
name: portal-arcade-reporter
description: Use this skill when Codex needs to answer read-only Portal Arcade gameplay and leaderboard questions across arcade games such as Brood Tapper and Hack Thy Sack, including current top scores, all-time high scores, highest scores for a specific day, high score for each configured game, games played today or yesterday, unique players, game-specific stats, average score, or daily activity summaries through each game's /api/agent reporting API.
---

# Portal Arcade Reporter

Use the Portal Arcade read-only agent APIs to answer gameplay reporting questions across one or more arcade games. Do not submit scores, modify game data, or expose internal identifiers.

More Portal Arcade games may be added over time. Prefer the game registry in this skill, and extend it with the same contract when a new game provides its own base URL and /api/agent routes.

## Configuration

Use these runtime environment variables:

- `ARCADE_AGENT_API_KEY`: shared bearer token for all Portal Arcade `/api/agent/*` routes.
- `BROOD_TAPPER_BASE_URL`: Brood Tapper app base URL, without a trailing slash when possible.
- `HACK_THY_SACK_BASE_URL`: Hack Thy Sack app base URL, without a trailing slash when possible.

If `ARCADE_AGENT_API_KEY` is missing, report the missing configuration and stop. If a requested game's base URL is missing, report that specific missing variable. For multi-game requests such as "high score for each game", query every configured game and mention any game skipped because its base URL is not configured.

Do not use the old Brood-only token names. Brood Tapper and Hack Thy Sack both use `ARCADE_AGENT_API_KEY`.

## Game Registry

Current games:

- Brood Tapper: base URL env `BROOD_TAPPER_BASE_URL`; route prefix `/api/agent`; score extras may include `glasses`.
- Hack Thy Sack: base URL env `HACK_THY_SACK_BASE_URL`; route prefix `/api/agent`; score fields include `durationMs` but no glasses metric.

When adding a future game, require its own `*_BASE_URL`, use the shared `ARCADE_AGENT_API_KEY`, and confirm it follows the same `/api/agent/scores` and `/api/agent/days` contract before using this workflow.

## API Contract

All requests are authenticated with:

`Authorization: Bearer $ARCADE_AGENT_API_KEY`

Available read-only endpoints for each configured game:

- `GET /api/agent/scores?scope=all-time&limit=10`: highest completed games across all time. `limit` defaults to 10 and must not exceed 100.
- `GET /api/agent/scores?scope=day&date=YYYY-MM-DD&tz=America/Denver&limit=10`: highest completed games during a calendar day interpreted in the requested IANA timezone. `date` is required; `limit` defaults to 10 and must not exceed 100.
- `GET /api/agent/days?date=YYYY-MM-DD&tz=America/Denver`: daily summary stats for a calendar day interpreted in the requested IANA timezone.

Expected score fields: `rank`, `handle`, `score`, `durationMs`, `playedAt`. Brood Tapper may also return `glasses`.

Expected daily summary fields: `date`, `tz`, `startsAt`, `endsAt`, `gamesPlayed`, `uniquePlayers`, `highestScore`, `averageScore`, `topScores`. Brood Tapper may also return `totalGlasses`.

Portal Arcade data models can include internal UUIDs, Portal profile ids, player ids, game ids, and launch token claims. Agent responses should expose only handles, score fields, game-specific public stats, and play timestamps. Never expose `profile_id`, raw launch token claims, or internal player/game ids if they appear in unexpected payloads.

## Query Routing

Choose games and endpoints from the user's question:

- If the user names a game, query only that game.
- If the user asks about Portal Arcade, arcade leaderboard, all games, or "each game", query all configured games.
- Current top ten, top scores, leaderboard, all-time high score: use `/api/agent/scores?scope=all-time`.
- Highest score today, yesterday, on a named date, or daily leaderboard: use `/api/agent/scores?scope=day`.
- Games played, how active, unique players, total glasses, average score, daily summary: use `/api/agent/days`.
- For questions that ask both participation and top score for a day, prefer `/api/agent/days` because it includes summary stats and `topScores`.
- For "high score for each game", use all-time scores with `limit=1` for every configured game unless the user specifies a date.

## Dates And Timezones

Resolve relative dates before calling the API:

- `today`: current date in the reporting timezone.
- `yesterday`: previous calendar date in the reporting timezone.
- Named weekdays: use the most recent matching weekday unless the user clearly means a future date.

Use the user's timezone if provided. If not provided, default to `America/Denver` for Raid Guild event reporting. The APIs interpret `date` in `tz`, convert that local day to UTC bounds, and query completed game timestamps using an inclusive start and exclusive end.

Treat `playedAt` as UTC unless a response includes local date metadata. When helpful, say which date and timezone the answer used.

## Request Pattern

Use Node's built-in `fetch` when shell HTTP tools are unavailable:

```js
const games = {
  brood: { label: 'Brood Tapper', base: process.env.BROOD_TAPPER_BASE_URL },
  hackThySack: { label: 'Hack Thy Sack', base: process.env.HACK_THY_SACK_BASE_URL },
};
const token = process.env.ARCADE_AGENT_API_KEY;
if (!token) throw new Error('Missing ARCADE_AGENT_API_KEY');

const game = games.hackThySack;
if (!game.base) throw new Error('Missing HACK_THY_SACK_BASE_URL');
const url = new URL('/api/agent/scores', game.base.replace(/\/$/, ''));
url.searchParams.set('scope', 'all-time');
url.searchParams.set('limit', '1');
const res = await fetch(url, { headers: { Authorization: `Bearer ${token}` } });
const text = await res.text();
if (!res.ok) throw new Error(`${game.label} API failed: ${res.status} ${text.slice(0, 200)}`);
const data = JSON.parse(text);
```

Handle `401` as unauthorized credentials. Handle empty score arrays as no completed games for that period. For multi-game questions, keep going if one configured game fails, then report the successful results and the failed game status without exposing tokens or debug internals.

## Reporting Style

Answer concisely. Include the game name with every score or summary when more than one game is involved. Include the concrete date and timezone for day-based results.

For score lists, show rank, handle, score, duration, played time, and game-specific public stats when present, such as Brood Tapper glasses. For daily summaries, show games played, unique players, highest score, average score, and game-specific public totals when present, such as total glasses.

Do not mention bearer tokens, local paths, internal APIs beyond the Portal Arcade route names, or implementation/debug details in the final answer.
