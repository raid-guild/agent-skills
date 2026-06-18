# Workflow Recipes

This directory contains normalized workflow recipes derived from Prism workflow exports.

The original exports remain immutable source material under `references/prism-workflows/`. Recipes here are the refactored working models that compose the durable RaidGuild skills in `skills/`.

## Node Types

- `agent`: Codex/agent work node.
- `gate`: human gate for steering, review, approval, rejection, or pause.
- `checkpoint`: long-running or indeterminate external job checkpoint.

## Execution Semantics

- A workflow whose first node is a human `gate` waits for human input before agent work starts.
- Human `gate` nodes always wait.
- `autoRun: true` on an `agent` node means the step may continue automatically when reached.
- `autoRun: false` on an `agent` node means the workflow waits for an operator to continue/start that agent step.
- `checkpoint` nodes wait for external job state, webhook/event reconciliation, or operator confirmation before routing onward.

## Current Recipes

- `blog-editorial-publish`: canonical editorial/blog workflow with generic, steered, fireside, and lore source modes.
- `brief-media-publish`: canonical brief, podcast, and recap media workflow with optional TTS/render path.
- `crm-document-ingest`: canonical Nexus CRM document handoff and metadata enrichment workflow.
- `dao-share-distro-proposal`: canonical DAO share distribution evidence and proposal workflow.
- `field-notes-from-fireside`: canonical Fireside parent workflow for source packages, calendar drafts, and non-autostart child requests.
- `fireside-wiki-topic-develop`: canonical Portal wiki topic workflow from fireside/research seeds.
- `meeting-transcript-memory-ingest`: narrow human-assisted Prism Memory transcript ingest workflow using Prism built-ins.
- `portal-activity-report`: canonical Portal activity, feedback, and arcade reporting workflow.
- `portal-session-recording-complete`: canonical Portal recording artifact ingest and recurrence workflow.
- `queen-raida-article-publish`: Queen Raida repo article workflow using Prism built-in `target-deploy-ops`.
- `queen-raida-social-graph-ops`: Queen Raida follow/account-graph workflow separated from social publishing.
- `queen-raida-social-publish`: canonical Queen Raida social workflow for replies, posts, threads, announcements, and campaign beats.
