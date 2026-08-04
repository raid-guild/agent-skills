---
name: rg-scribe-publisher-skill
description: Use when a workflow or user explicitly requests the RG Scribe publishing pass to draft, adapt, or polish source-grounded RaidGuild public copy. Coordinates content strategy and brand voice for blog, Portal, newsletter, Discord, announcement, recap, and project-note drafts; it does not research facts, approve safety, or publish.
---

# RG Scribe Publisher

Turn approved source material into clear, credible RaidGuild publishing copy.

## Required sequence

1. Read the source material, audience, channel, and approval context.
2. Use `rg-content-strategy` to confirm the content job, angle, structure, and missing facts.
3. Draft or revise with concrete facts before promotional language.
4. Use `rg-brand-voice` for the selected RaidGuild voice layer and prose polish.
5. Preserve uncertainty, source notes, and explicit placeholders. Never invent facts, quotes, metrics, names, dates, clients, outcomes, or publishing status.
6. Hand public-ready copy to `rg-public-output-safety`. Do not mark it safe or publish it from this skill.

## Editing rules

- Prefer specific evidence to broad claims.
- Cut throat-clearing, hype, corporate phrasing, repeated conclusions, and machine-like transitions.
- Keep useful builder-native roughness when it improves credibility.
- Use mythic or cultural texture only after the concrete point is clear.
- Preserve exact quotes only when the source wording is verified; otherwise paraphrase.
- Keep internal workflow notes out of reader-facing copy.

## Output

Return the draft or revision plus:

- audience and channel
- selected voice layer
- source notes or unresolved factual risks
- a concise changelog when revising
- a clear handoff stating that public-output safety review is still required
