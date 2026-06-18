---
name: rg-content-strategy
description: Use when Codex needs to plan, frame, adapt, or evaluate RaidGuild content strategy, including content pillars, campaign angles, source-to-draft planning, editorial briefs, channel formats, content QA, repurposing plans, X/Discord/blog/newsletter concepts, Queen Raida campaign framing, AI Solutions content planning, and workflow-to-public-output strategy. Not for brand voice polish, safety sanitization, live publishing, API operations, or unsourced current-event claims by itself.
---

# RaidGuild Content Strategy

Use this skill to decide what to say, why it matters, who it is for, and what shape it should take.

This skill owns strategy, editorial framing, content structure, channel fit, and source-to-draft planning. It does not own final voice polish, public safety review, API posting, or live system operations.

## Modes

- `BUILD`: create a campaign plan, content pillar map, editorial brief, or repeatable content recipe.
- `ADAPT`: convert source material or an existing draft to another channel or audience.
- `AUDIT`: evaluate a draft, plan, or workflow for strategy, evidence, audience fit, and channel fit.
- `BRIEF`: turn raw context into a draft brief for another writer, agent, or workflow.

## Routing

Read only the references needed for the task:

- Editorial strategy and rubrics: `references/editorial-rubric.md`
- Source-to-draft planning: `references/source-to-draft.md`
- Channel formats: `references/channel-formats.md`
- Content pillars: `references/content-pillars.md`
- Workflow patterns: `references/workflow-patterns.md`
- Repo-level voice source model: `docs/voice-corpus-plan.md`

Use `rg-brand-voice` after strategy when the task needs final RaidGuild voice or persona fit.

Use `rg-public-output-safety` before public output is posted, queued, or marked ready for approval.

Use research or live Prism Memory only when current facts, receipts, or recent community activity are needed. Strategy should not invent missing facts.

## Strategy Workflow

1. Identify audience, channel, purpose, and approval context.
2. Separate source facts from interpretation.
3. Choose the content job: announce, explain, recap, invite, prove, recruit, sell, document, or respond.
4. Pick the voice layer to hand off to `rg-brand-voice`.
5. Select format and structure from the channel references.
6. Define missing facts and blockers before drafting.
7. Draft a brief, outline, angle set, or content plan.
8. Add review gates for public, client, governance, financial, or security-sensitive output.

## Default Principles

- One concrete signal before one broad claim.
- Do not make one workflow into a whole campaign unless there is audience value.
- Prefer source-backed angles over generic thought leadership.
- Keep public claims no more specific than the evidence allows.
- Separate strategy from publishing mechanics.
- For Queen Raida, make the useful operational point first and the weird texture second.
- For AI Solutions, prioritize buyer clarity, offer fit, and proof discipline.

## Output

For plans, return:

- `audience`
- `channel`
- `contentJob`
- `angle`
- `sourceFacts`
- `missingFacts`
- `recommendedFormat`
- `draftBrief`
- `reviewGates`

For audits, return:

- `strategicFit`
- `sourceSupport`
- `channelFit`
- `risks`
- `recommendedChanges`
