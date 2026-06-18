# Queen Raida Social Publish

This workflow turns source-backed RaidGuild, Portal, cohort, member, project, support, or campaign context into Queen Raida social output.

Use it for:

- replies to X collection summaries or specific posts
- new posts or short threads
- campaign beats such as Portal launch updates
- lightweight public support responses
- announcements that should come from `@raidguildish`

Do not use it for:

- following, unfollowing, blocking, or account graph changes
- publishing long-form Queen Raida website articles
- posting as the official `@RaidGuild` HQ account unless a human explicitly changes the account and the copy is re-reviewed for that persona
- unsupported project, governance, launch, client, or member claims

## Canonical Shape

1. Human steering gate confirms source, target account, target action, and mode.
2. Source intake builds a facts-first brief.
3. Strategy selects the social angle, target action, and Queen Raida texture level.
4. Draft produces candidate public text.
5. Safety pass checks public risk before review.
6. Human review approves exact text and target action.
7. Publish or queue runs only after explicit approval and operator continuation.
8. Reconcile records posted/queued URLs and evidence.

## Source Modes

- `response`: source-backed reply or quote to a post/thread.
- `new_post`: standalone post from a source pack or verified update.
- `thread`: short sequence where one post cannot carry the context clearly.
- `campaign`: one beat in a larger public campaign.
- `support`: public clarification or lightweight support response.
- `announcement`: public update with concrete facts and destination links.

## Skill Composition

- `rg-content-strategy`: source-to-angle, audience, format, and campaign fit.
- `rg-brand-voice`: Queen Raida persona, RaidGuild voice fit, and channel tone.
- `rg-public-output-safety`: sanitizer and blocker contract.
- `rg-publishing-ops`: X queue/API, Discord summary, schedule or publish evidence.
- `rg-portal-ops`: Portal facts and URLs when the post references Portal content.

## Operator Semantics

The first node is a human gate, so the workflow waits before any agent work starts. Agent nodes may run automatically after steering, but the publish node has `autoRun: false`; an operator must continue it after approving exact text, account, and action.

If a parent campaign workflow spawns this workflow, set the child request to `autoRun: false` when the spawned request needs human steering before intake.
