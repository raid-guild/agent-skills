---
name: rg-publishing-ops
description: Use when Codex needs to prepare, inspect, schedule, queue, send, publish, or reconcile approved RaidGuild publishing operations across Bard Calendar, Discord, X, X draft queue, public CMS/blog workflows, newsletters, campaign calendars, live URLs, draft URLs, and post-publication status. Requires public-output safety before public posting or queueing. Not for writing strategy, brand voice polish, Portal CMS content modeling, or unsafe live publication without approval.
---

# RaidGuild Publishing Ops

Use this skill for publishing mechanics after content strategy, voice, and safety are handled.

This skill owns calendars, queueing, sends, destination resolution, approval gates, status changes, and live URL reconciliation. It does not own content strategy, voice, public safety review, or Portal CMS record modeling.

## Operating Rule

Do not publish, send, queue, or mark content as published unless:

1. the output has passed `rg-public-output-safety`;
2. the destination/account/channel is explicit;
3. the approval gate is satisfied in the current request or workflow;
4. the exact text, target, and timing are known.

When in doubt, prepare a publishing plan and stop for approval.

## Routing

Read only the references needed:

- Approval gates: `references/publish-approval-gates.md`
- Bard Calendar: `references/bard-calendar.md`
- Discord send: `references/discord-send.md`
- X draft queue: `references/x-draft-queue.md`
- X API operations: `references/x-api.md`
- Live URL reconciliation: `references/live-url-reconciliation.md`

Use `rg-content-strategy` for what to say.
Use `rg-brand-voice` for how it should sound.
Use `rg-public-output-safety` before anything public is sent or queued.
Use `portal-ops` for Portal CMS records, post drafts, wiki pages, sessions, and Portal artifacts.

## Modes

- `PLAN`: prepare destination, timing, approval, and status plan.
- `SCHEDULE`: create or update calendar/planning records.
- `QUEUE`: add approved X/social draft to an autonomous or scheduled queue.
- `SEND`: send approved Discord/channel output.
- `PUBLISH`: perform an approved live publishing action through the relevant API.
- `RECONCILE`: update status, live URL, draft URL, failures, and evidence after publish.
- `REPORT`: inspect calendars, queues, or publishing status.

## Safety Defaults

- Public output must pass `rg-public-output-safety` before `QUEUE`, `SEND`, or `PUBLISH`.
- Discord sends require explicit destination resolution.
- X queue entries must already be approved for autonomous posting.
- Do not mark Bard Calendar events as `published` without a live URL, external evidence, or explicit user confirmation.
- Do not expose API tokens, adapter tokens, raw auth headers, or private artifact URLs.
- For governance, treasury, production, security, client, or public announcement content, restate destination and content summary before live send unless the workflow is already at an approved publish step.

## Output

For plans:

```text
Publishing plan:
- content:
- destination:
- account/persona:
- timing:
- approval status:
- safety status:
- operation:
- evidence to capture:
- blockers:
```

For completed operations, report:

- operation performed
- destination/account
- returned id or URL
- calendar/queue/status updates
- failures or retry guidance
