---
name: rg-research
description: Use when Codex needs RaidGuild research discipline, source discovery, current-signal scouting, Hacker News scanning, Hivemind/context lookup, source ledgers, claim verification, confidence labels, or evidence briefs before strategy, drafting, wiki work, public commentary, campaign planning, or workflow decisions. Not for final brand voice, public safety sanitization, publishing, Portal writes, or broad content planning by itself.
---

# RaidGuild Research

Use this skill to find, verify, rank, and explain sources before downstream strategy, drafting, publishing, or operations.

This skill owns research behavior: source discovery, source quality, current-signal scouting, claim checking, evidence ledgers, and confidence labeling. It does not own final voice, public safety review, live publishing, CMS writes, or financial/onchain operations.

## Modes

- `DISCOVER`: find relevant sources or current signals.
- `VERIFY`: check whether a claim is supported, outdated, uncertain, or false.
- `SCOUT`: scan HN/current public sources for relevant angles.
- `LEDGER`: turn source material into an evidence ledger for another workflow.
- `BRIEF`: synthesize findings into a compact research brief.

## Routing

Read only the references needed for the task:

- Source ledger format: `references/source-ledger.md`
- Claim confidence and verification: `references/claim-confidence.md`
- Current-signal ranking: `references/current-signal-ranking.md`
- Hacker News scouting/API: `references/hacker-news.md`
- DuckDuckGo/ddgs fallback: `references/duckduckgo-ddgs.md`
- Hivemind usage boundary: `references/hivemind-context.md`

Use `rg-content-strategy` after research when the task needs positioning, content angle, or channel planning.

Use `rg-brand-voice` after research and strategy when output needs RaidGuild, AI Solutions, or Queen Raida voice.

Use `rg-public-output-safety` before public output is posted, queued, or marked ready.

## Default Source Order

1. Use task-provided sources first.
2. Use repo, Prism, Portal, or Hivemind context only when the task gives access or asks for that context.
3. Use built-in web search/browsing when current public facts or source discovery are required.
4. Use the official Hacker News API for HN-native scouting.
5. Use `ddgs`/DuckDuckGo only as a fallback or provider-specific path after verifying the runtime supports it.
6. Prefer primary sources over summaries, comments, social posts, or snippets.

## Research Workflow

1. Identify the question, claim, audience, recency requirement, and allowed source classes.
2. Separate source discovery from source extraction.
3. Read primary sources before making a claim when the answer depends on details.
4. Record direct evidence, interpretation, and open questions separately.
5. Label confidence for each important claim.
6. Flag missing, stale, private, unverifiable, or contradictory evidence.
7. Return a source ledger or research brief that downstream skills can use without redoing discovery.

## Defaults

- Current or unstable facts require live verification.
- Search result snippets are leads, not evidence.
- HN comments are signal, not verified fact.
- Hivemind is strategy/context input, not factual authority by itself.
- If sources conflict, report the conflict instead of smoothing it over.
- Do not invent RaidGuild, client, member, governance, project, or product facts from weak signals.

## Output

For research briefs, return:

- `question`
- `sourceSet`
- `keyFindings`
- `claimConfidence`
- `sourceLedger`
- `openQuestions`
- `recommendedNextStep`

For claim checks, return:

- `claim`
- `verdict`
- `confidence`
- `supportingSources`
- `contradictingSources`
- `notes`
