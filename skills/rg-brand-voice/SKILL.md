---
name: rg-brand-voice
description: Use when Codex needs to draft, revise, adapt, or audit RaidGuild-aligned language for brand voice, prose mechanics, tone, persona fit, AI-tell cleanup, channel voice, AI Solutions copy, Queen Raida copy, community-facing updates, website copy, sales collateral, social posts, newsletters, or public/internal communications. Not for publishing actions, API calls, source research, live memory lookup, or safety sanitization by itself.
---

# RaidGuild Brand Voice

Use this skill to make RaidGuild writing sound like RaidGuild without flattening every context into the same voice.

This skill owns voice, prose, tone, persona overlays, and language anti-patterns. It does not own content strategy, fact research, public safety review, or live publishing operations.

## Modes

- `BUILD`: create or update a voice reference from reviewed source material.
- `ADAPT`: adapt a draft to a channel, audience, or persona.
- `AUDIT`: evaluate existing copy against voice rules and anti-patterns.
- `POLISH`: rewrite a draft while preserving source facts and intent.

## Routing

Read only the references needed for the task:

- Core RaidGuild voice: `references/raidguild-core-voice.md`
- AI Solutions/buyer-facing voice: `references/ai-solutions-voice.md`
- Queen Raida persona voice: `references/queen-raida-voice.md`
- Channel modulation: `references/channel-voice.md`
- Language anti-patterns and AI tells: `references/language-anti-patterns.md`
- Voice source/corpus model: repo-level `docs/voice-corpus-plan.md`

If the task asks for current facts, source discovery, or live Prism Memory context, use the relevant research/memory workflow before writing. Do not invent facts to satisfy voice.

If the output may become public, route the final draft through `rg-public-output-safety` before publishing, queueing, or presenting as ready.

## Voice Selection

Before rewriting, choose the voice layer:

1. `RaidGuild core`: public brand, community updates, general site copy.
2. `AI Solutions`: buyer-facing offers, sales collateral, service pages, launch notes.
3. `Queen Raida`: `@raidguildish`, agent persona, agent capability updates.
4. `Internal/community`: Discord, coordination notes, review asks, member-facing summaries.

Score the draft on:

- formality: tavern/native to institutional/client-safe
- weirdness: plain operator to mythic/occult/zine
- specificity: broad pattern to named receipts
- authority: tentative draft to confident statement
- persona: RaidGuild generic to named agent/persona

Choose the score before rewriting.

## Default Rules

- Put concrete facts before mythic texture.
- Preserve uncertainty when source material is incomplete.
- Use lore as seasoning, not as a substitute for meaning.
- Replace generic AI/SaaS phrasing with specific builder-native language.
- Do not let Queen Raida speak as `@RaidGuild` HQ or as a human member.
- Do not use buyer-safe AI Solutions voice for community tavern copy unless the user asks.
- Do not turn rough builder language into sterile brand mush.

## Output

For audits, return:

- `voiceFit`: short assessment
- `selectedVoiceLayer`: one of the layers above
- `issues`: concrete voice, prose, or anti-pattern findings
- `revisedDraft`: if requested
- `safetyNotes`: only voice-adjacent concerns; defer full safety review to `rg-public-output-safety`

For rewrites, return the revised draft plus a concise change note when useful.
