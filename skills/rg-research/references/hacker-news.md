# Hacker News

Use the official Hacker News Firebase API for HN-native scouting.

Source:

- Docs: `https://github.com/HackerNews/API`
- Base: `https://hacker-news.firebaseio.com/v0`
- Human item URL: `https://news.ycombinator.com/item?id=<id>`

## Useful Endpoints

- `/topstories.json`
- `/beststories.json`
- `/newstories.json`
- `/showstories.json`
- `/askstories.json`
- `/jobstories.json`
- `/item/<id>.json`
- `/user/<id>.json`

## Scouting Procedure

1. Fetch a bounded sample from top, best, and new stories.
2. Fetch item details for each story.
3. Deduplicate by item id and URL.
4. Score for RaidGuild relevance, freshness, score/comment count, operational lesson, and public-safety risk.
5. Read the original source article before making factual claims beyond HN metadata.
6. Treat comments as context and sentiment, not verified fact.

## Relevance Areas

- AI agents, LLM tooling, evals, MCP, workflow automation
- memory, retrieval, source provenance, knowledge systems
- developer tools, open source, maintainers, package ecosystems
- governance, coordination, communities, public goods
- publishing, CMS, search, social platforms
- security, privacy, moderation, infrastructure incidents

## Output

For each recommended item:

- title
- source URL
- HN discussion URL
- score/comment count/time
- why it matters
- RaidGuild or Queen Raida angle
- safety notes
- optional draft seed
