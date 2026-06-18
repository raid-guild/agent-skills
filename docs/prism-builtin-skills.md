# Prism Built-In Skills

Some capabilities should remain Prism environment built-ins rather than RaidGuild portable skills in this repo.

Source references:

- Prism Memory built-ins: `https://github.com/superprismio/prism-railway-template/tree/main/services/prism-memory/skills`
- Prism Site built-ins: `https://github.com/superprismio/prism-railway-template/tree/main/services/site/skills`

## Prism Memory Service

These are built into the Prism Memory service:

- `prism-api-ops`
- `prism-api-reader`
- `prism-api-writer`
- `prism-config-admin`
- `prism-discord-promote-doc`
- `prism-knowledge-sources`

Use these for deployed Prism Memory API reads, writes, config/admin work, knowledge source management, and Discord-to-memory/knowledge promotion.

This repo should not duplicate those endpoint contracts unless a reusable RaidGuild policy layer is needed.

## Prism Site Service

These are built into the Prism site service:

- `change-request-ops`
- `prism-hook-author`
- `prism-instance-profile`
- `prism-instance-settings`
- `prism-scheduled-task-runner`
- `prism-skill-author`
- `prism-task-author`
- `prism-workflow-author`
- `target-deploy-ops`

Use these for request/workflow state, source attachments, workflow continuation, target app metadata, repo work, deploy plans, staging deploys, and Prism authoring.

## Boundary

Portable RaidGuild skills should compose with these built-ins instead of copying them.

Examples:

- `meeting-transcript-memory-ingest` should use `prism-api-writer` and `change-request-ops` in Prism runtime.
- `queen-raida-article-publish` should use `target-deploy-ops` for repository/deploy work.
- Workflow import/export mechanics should use `prism-workflow-author` when operating inside Prism.
