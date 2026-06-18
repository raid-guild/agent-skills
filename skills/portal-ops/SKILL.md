---
name: portal-ops
description: Use when Codex needs to inspect, plan, create, or update RaidGuild Portal CMS records through safe Payload API workflows, including sessions/events, posts, wiki pages, briefs, projects, threads, activity items, profiles, spotlights, CMS-managed page copy, event artifacts, resources, and source-grounded memory updates. Prefer reviewable plans and drafts unless the target environment, source facts, account, and approval are clear. Not for general content strategy, brand voice polish, or non-Portal publishing sends.
---

# RaidGuild Portal Ops

Use this skill for Portal CMS and Payload API operations.

The Portal is the presentation and coordination layer for real community activity. Do not invent activity, project state, people, dates, links, sources, claims, decisions, or approvals.

## Operating Rule

Default to a reviewable create/update plan. Write directly to Payload only when the user explicitly asks, the target environment is clear, and the operation is safe.

When writing as automation, use a dedicated agent account. Do not use a human contributor account for automated publishing.

## Routing

Read only the references needed:

- Portal primitives: `references/primitives.md`
- Event creation, sessions, and Discord sync: `references/events-and-discord-sync.md`
- Event artifact ingest and resources: `references/artifact-ingest.md`
- Posts and images: `references/posts-and-images.md`
- Wiki pages: `references/wiki-pages.md`
- CMS page copy: `references/page-copy.md`
- Confidence, create/update rules, and output shape: `references/confidence-and-review.md`

Use repo-level `references/portal-cms-model.md` when field-level detail is needed.
Use repo-level `references/example-digest-mapping.md` for example memory-to-Portal mapping.

Use `rg-content-strategy` before Portal post/wiki drafting when the angle is unclear.
Use `rg-brand-voice` before final public copy.
Use `rg-public-output-safety` before publishing public Portal content.
Use `rg-publishing-ops` for non-Portal sends, queues, calendars, and live URL reconciliation.

## Source Inputs

Use for:

- Discord channel summaries
- meeting digests or transcripts
- project updates
- event/session notes
- repo activity summaries
- community memory rollups
- content or wiki research packets
- CMS-managed copy changes
- session resources, comments, and artifact updates

If input lacks timestamps, participants, sources, or approval, preserve uncertainty and draft the record instead of publishing it.

## Workflow

1. Extract factual signals from source material.
2. Identify existing projects, threads, events, profiles, posts, or wiki pages that should be updated.
3. Prefer updating existing continuity records over creating duplicates.
4. Create new records only when the source introduces a distinct real object.
5. Choose draft vs publish using confidence and approval rules.
6. Produce a reviewable create/update plan unless direct write is explicitly approved.
7. If writing, capture ids, URLs, status, and response evidence.

## Guardrails

- Keep projects as collaboration surfaces, not task boards.
- Do not create tasks, assignees, sprint boards, estimates, or PM workflow state.
- Keep activity short, dated, and source-grounded.
- Keep threads lightweight; they are continuity, not categories or tickets.
- Create or update wiki pages only when the source supports durable topic knowledge, not transient recap content.
- Use posts for reviewed editorial or distribution artifacts.
- Do not publish wiki pages unless `reviewStatus` is `reviewed`.
- Do not create or update admin-only wiki pages as an agent.
- Do not delete records unless explicitly requested and confirmed.

## Output

Use the output shape in `references/confidence-and-review.md` unless the user requests direct edits.
