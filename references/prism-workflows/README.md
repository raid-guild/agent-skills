# Prism Workflow Reference Export

This directory contains reference copies of enabled instance workflows exported from the Prism site service on 2026-06-18.

These files are source material for workflow migration and review. They are not runtime workflow state, and approval/current-step/run history remains owned by Prism database records.

## Source

- Source service: Prism site service workflow API
- List endpoint: `GET /agent/workflows`
- Detail endpoint pattern: `GET /agent/workflows/<workflow-key>`
- Auth used for export: service-token auth from the agent runtime environment

Built-in system-default workflows and disabled workflows are intentionally excluded from this reference export unless separately requested.

Runtime filesystem paths from Prism workflow definitions are normalized in `manifest.proposal.json` so each workflow uses local repository paths: `workflow.md` and `steps/<step-key>.md`.

## Exported Workflows

| Workflow | Version | Step files | Reference copy |
| --- | ---: | ---: | --- |
| blog-post-draft-review-publish | 9 | 9/10 | references/prism-workflows/blog-post-draft-review-publish/ |
| blog-post-steered-draft-review-publish | 6 | 9/10 | references/prism-workflows/blog-post-steered-draft-review-publish/ |
| crm-document-ingest-enrich | 3 | 1/2 | references/prism-workflows/crm-document-ingest-enrich/ |
| daily-memory-brief-review | 3 | 4/5 | references/prism-workflows/daily-memory-brief-review/ |
| field-notes-from-fireside | 17 | 8/9 | references/prism-workflows/field-notes-from-fireside/ |
| fireside-blog-post-draft-publish | 13 | 6/7 | references/prism-workflows/fireside-blog-post-draft-publish/ |
| fireside-recap-video-publish | 1 | 9/10 | references/prism-workflows/fireside-recap-video-publish/ |
| fireside-wiki-topic-develop | 4 | 9/10 | references/prism-workflows/fireside-wiki-topic-develop/ |
| internal-daily-brief-podcast-publish | 7 | 11/11 | references/prism-workflows/internal-daily-brief-podcast-publish/ |
| lore-entry-draft-review-publish | 2 | 9/10 | references/prism-workflows/lore-entry-draft-review-publish/ |
| meeting-transcript-memory-ingest | 1 | 2/3 | references/prism-workflows/meeting-transcript-memory-ingest/ |
| monthly-share-distro-proposal | 6 | 6/7 | references/prism-workflows/monthly-share-distro-proposal/ |
| portal-session-recording-complete | 4 | 4/5 | references/prism-workflows/portal-session-recording-complete/ |
| publish-queen-raida-article | 1 | 2/5 | references/prism-workflows/publish-queen-raida-article/ |
| queen-raida-portal-launch-campaign | 3 | 7/8 | references/prism-workflows/queen-raida-portal-launch-campaign/ |
| queen-raida-x-follow-scout-review-follow | 1 | 4/4 | references/prism-workflows/queen-raida-x-follow-scout-review-follow/ |
| queen-raida-x-response-draft-review-publish | 5 | 4/5 | references/prism-workflows/queen-raida-x-response-draft-review-publish/ |
| weekly-portal-activity-snapshot | 1 | 3/4 | references/prism-workflows/weekly-portal-activity-snapshot/ |
| weekly-public-brief-podcast-publish | 9 | 11/11 | references/prism-workflows/weekly-public-brief-podcast-publish/ |

## Excluded Workflows

| Workflow | Reason |
| --- | --- |
| change-request-default | system default |
| temp-probe | disabled |

## Content Notes

- fireside-recap-video-publish: workflow-level markdown was not available; generated workflow.md from name/description.

## Refresh Process

1. Query `GET /agent/workflows` with `x-service-token` service auth.
2. Filter to enabled, non-system workflows unless the export scope changes.
3. Fetch each workflow with `GET /agent/workflows/<workflow-key>`.
4. Write a normalized `manifest.proposal.json`, `workflow.md`, available `steps/*.md`, and `source.json` under `references/prism-workflows/<workflow-key>/`.
5. Update this index with the new export date, workflow list, and any missing-content notes.
6. Review the diff for secrets, private client context, runtime artifacts, generated outputs, and accidental disabled/system workflow exports.
