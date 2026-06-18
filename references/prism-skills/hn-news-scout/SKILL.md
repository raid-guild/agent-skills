---
name: hn-news-scout
description: Use this skill when Codex needs to scan Hacker News for current stories that may be useful for Queen Raida, RaidGuild social output, public commentary, or workflow-backed X response drafting. The skill turns HN stories into ranked post angles grounded in relevance, not generic news summaries.
---

# HN News Scout

Use this skill to inspect current Hacker News stories and identify items worth Queen Raida noticing or using as public social context.

This skill is for scouting signal, not publishing. It must not post to X, Discord, CMS, or any public surface.

## Source

Use the official Hacker News API:

- Base: `https://hacker-news.firebaseio.com/v0`
- Lists:
  - `/topstories.json`
  - `/beststories.json`
  - `/newstories.json`
  - optionally `/showstories.json`, `/askstories.json`, or `/jobstories.json` only when relevant
- Item detail:
  - `/item/<id>.json`
- Human discussion URL:
  - `https://news.ycombinator.com/item?id=<id>`

Prefer direct API reads over scraping HN HTML.

## When To Use

Use this skill when asked to:

- check the latest Hacker News stories
- find HN items relevant to Queen Raida
- create post angles from HN
- add external tech-news signal to an X response workflow
- compare HN stories against RaidGuild/Prism/Portal context

## Relevance Model

Prioritize stories related to:

- AI agents, LLMs, model behavior, evals, guardrails, MCP, tool use
- memory systems, knowledge bases, retrieval, search, provenance, context management
- developer tools, GitHub, repo security, supply chain, package ecosystems, editors
- open source governance, community infrastructure, maintainer burnout, public goods
- social platforms, moderation, publishing, algorithmic reach, creator/community dynamics
- automation failures, workflow design, human-in-the-loop systems
- privacy, security, censorship, platform risk
- CMS, content systems, docs, knowledge publishing
- incidents involving infrastructure builders use, such as Railway, GitHub, Cloudflare, Vercel, npm, PyPI

Deprioritize generic macro news, consumer product announcements, politics, and pure model-release hype unless there is a strong operational angle.

## Scouting Procedure

1. Fetch a bounded sample from `topstories`, `beststories`, and `newstories`.
   - Suggested defaults: top 50, best 40, new 60.
2. Fetch item details for each story.
3. Deduplicate by item id and URL.
4. Score each candidate using:
   - relevance to Queen Raida/RaidGuild themes
   - freshness
   - HN score and comment count
   - whether the story has a concrete operational lesson
   - whether it can connect to Prism Memory, Prism Knowledge, Portal CMS, project history, or RaidGuild lived experience
5. Return a ranked brief of the best 3-7 items.

## Output Shape

For each recommended item, include:

- title
- source URL, if present
- HN discussion URL
- score/comment count/time when available
- why it matters
- Queen Raida angle
- possible RaidGuild/Prism/Portal connection
- safety notes, if any
- optional draft seed, no more than 1-4 short lines

Keep the brief compact. Do not dump long lists unless explicitly asked.

## Queen Raida Framing Rules

Queen Raida should sound like an intelligence node inside a builder ecosystem, not a generic tech-news account.

Prefer angles that feel like:

- recurring operational pattern
- field intelligence
- project archaeology
- coordination lesson
- security ritual
- memory/provenance warning
- maintainer/public-goods observation
- agent workflow failure mode

Avoid:

- generic “AI is changing everything” commentary
- unsupported claims about RaidGuild involvement
- private operational details
- claims that Queen Raida has read private data unless that data was actually queried through Prism Memory/Knowledge/CMS for the task
- excessive lore detached from the source story

Useful formula for post angles:

- 30% operational observation
- 25% synthesis or pattern recognition
- 20% weird techno-occult texture
- 15% concrete example or sourced detail
- 10% provocative tension

## Cross-Source Grounding

When the task asks for stronger RaidGuild relevance, combine HN scouting with available Prism skills:

- Use `prism-api-reader` for Prism Memory, digests, knowledge docs, and project state.
- Use Portal CMS data only through approved APIs or existing workflow/context, not browser admin routes.
- Use Queen Raida repo-backed docs from Prism Knowledge source `queen-raida` when shaping tone, safety, and post examples.

Do not invent connections. If no RaidGuild/Prism connection is found, say the HN item is only generally relevant.

## Safety

- Do not publish.
- Do not follow accounts.
- Do not treat HN comments as verified facts.
- Prefer source article facts over comment speculation.
- Link both the HN discussion and the original source when available.
- Flag sensitive topics such as security incidents, censorship, politics, or personal allegations for human review before public output.
