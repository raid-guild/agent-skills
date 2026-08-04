---
name: rg-scribe-publisher-skill
description: Use when a workflow or user explicitly requests the RG Scribe publishing pass to draft, adapt, or polish source-grounded RaidGuild copy. Coordinates content strategy and brand voice for blog, Portal, newsletter, Discord, announcement, recap, and project-note drafts; only presents copy as public-ready after explicit human confirmation and safety review, and does not research facts or publish.
---

# RG Scribe Publisher

Turn approved source material into clear, credible RaidGuild publishing copy.

## Required sequence

1. Read the source material, audience, channel, and approval context. Confirm whether the task is creating a review draft or polishing human-approved material.
2. Use `rg-content-strategy` to confirm the content job, angle, structure, and missing facts.
3. Create a review draft, or revise material that a human has explicitly confirmed for public-ready treatment.
4. Use `rg-brand-voice` for the selected RaidGuild voice layer and prose polish.
5. Preserve uncertainty, source notes, and explicit placeholders. Never invent facts, quotes, metrics, names, dates, clients, outcomes, or publishing status.
6. Do not describe a review draft as public-ready. Require explicit human confirmation of the draft and source material first.
7. Hand confirmed copy to `rg-public-output-safety`. Do not mark it safe or publish it from this skill.

Keep prose and voice rules in `rg-brand-voice`; this skill owns only orchestration and handoff.

## Output

Return the draft or revision plus:

- audience and channel
- selected voice layer
- source notes or unresolved factual risks
- a concise changelog when revising
- a clear handoff stating that public-output safety review is still required
