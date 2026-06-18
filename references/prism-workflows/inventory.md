# Prism Workflow Inventory

This inventory tracks exported Prism workflows and their likely migration target.

Decisions:

- `keep-canonical`: keep as canonical workflow recipe.
- `merge`: merge behavior into a canonical workflow family.
- `workflow-reference`: keep as a recipe/reference, not a skill.
- `deprecate`: remove after replacement exists.
- `needs-review`: needs more product/operator review.

| Workflow | Version | Family | Old Skill Dependencies | Proposed New Skill Sequence | Decision | Notes |
| --- | ---: | --- | --- | --- | --- | --- |
| `blog-post-draft-review-publish` | 9 | blog/editorial publish | `prism-api-reader`, `portal-memory-publisher` | `rg-content-strategy` -> `rg-brand-voice` -> `rg-public-output-safety` -> `rg-portal-ops` | merge | Merged into `workflows/blog-editorial-publish` generic mode. |
| `blog-post-steered-draft-review-publish` | 6 | blog/editorial publish | `prism-api-reader`, `portal-memory-publisher` | `rg-content-strategy` -> `rg-brand-voice` -> `rg-public-output-safety` -> `rg-portal-ops` | keep-canonical | Base for `workflows/blog-editorial-publish` steering gate and steered mode. |
| `fireside-blog-post-draft-publish` | 13 | blog/editorial publish | `prism-api-reader`, `portal-ops-skill`, `rg-scribe-publisher-skill`, `public-social-output-sanitizer`, `x-developer-api`, `imagegen` | `rg-content-strategy` -> `rg-brand-voice` -> `rg-public-output-safety` -> `rg-portal-ops` plus `imagegen` | merge | Merged into `workflows/blog-editorial-publish` fireside mode. |
| `daily-memory-brief-review` | 3 | brief publish | `prism-api-reader` | `rg-content-strategy` -> `rg-brand-voice` -> `rg-public-output-safety` -> `rg-portal-ops` | merge | Merged into `workflows/brief-media-publish` brief-only/daily memory mode. |
| `weekly-public-brief-podcast-publish` | 9 | brief/podcast/media | `prism-api-reader`, `portal-memory-publisher` | `rg-content-strategy` -> `rg-brand-voice` -> `rg-public-output-safety` -> `s3-object-storage` -> `rg-media-render-ops` -> `rg-portal-ops` | keep-canonical | Base for `workflows/brief-media-publish` weekly public mode. |
| `internal-daily-brief-podcast-publish` | 7 | brief/podcast/media | `prism-api-reader`, `portal-memory-publisher`, `remotion-composition-checker`, `workflow-audio-bucket-uploader` | `rg-content-strategy` -> `s3-object-storage` -> `rg-media-render-ops` -> `rg-portal-ops` | workflow-reference | Merged into `workflows/brief-media-publish` internal daily mode; visibility rules stay mode-specific. |
| `field-notes-from-fireside` | 17 | fireside parent/orchestration | `prism-api-reader`, `portal-ops-skill`, `rg-scribe-publisher-skill`, `public-social-output-sanitizer`, `x-developer-api`, `change-request-ops`, `bard-calendar-ops` | `rg-content-strategy` -> `rg-brand-voice` -> `rg-public-output-safety` -> `rg-portal-ops` -> `rg-publishing-ops` | keep-canonical | Implemented as `workflows/field-notes-from-fireside`; parent spawns non-autostart blog, wiki, and recap-media child requests. |
| `fireside-recap-video-publish` | 1 | fireside media | `prism-api-reader`, `portal-ops-skill`, `remotion-composition-checker`, `workflow-audio-bucket-uploader`, `public-social-output-sanitizer` | `rg-content-strategy` -> `rg-brand-voice` -> `rg-public-output-safety` -> `s3-object-storage` -> `rg-media-render-ops` -> `rg-portal-ops` | workflow-reference | Merged into `workflows/brief-media-publish` fireside recap mode; still useful as a source-specific reference. |
| `fireside-wiki-topic-develop` | 4 | wiki/research | `prism-api-reader`, `portal-ops-skill`, `rg-scribe-publisher-skill`, `hn-news-scout`, `public-social-output-sanitizer`, `change-request-ops` | `rg-research` -> `rg-content-strategy` -> `rg-brand-voice` -> `rg-public-output-safety` -> `rg-portal-ops` | keep-canonical | Implemented as `workflows/fireside-wiki-topic-develop`. |
| `lore-entry-draft-review-publish` | 2 | lore/editorial publish | `prism-api-reader`, `queen-raida-social-agent`, `public-social-output-sanitizer`, `portal-memory-publisher` | `rg-content-strategy` -> `rg-brand-voice` -> `rg-public-output-safety` -> `rg-portal-ops` | merge | Merged into `workflows/blog-editorial-publish` lore mode. |
| `publish-queen-raida-article` | 1 | Queen Raida site/repo publish | `target-deploy-ops`, `public-social-output-sanitizer` | `rg-content-strategy` -> `rg-brand-voice` -> `rg-public-output-safety` plus Prism built-in `target-deploy-ops` | workflow-reference | Implemented as `workflows/queen-raida-article-publish`; uses Prism site built-in `target-deploy-ops`. |
| `queen-raida-portal-launch-campaign` | 3 | Queen Raida campaign/social publish | `prism-api-reader`, `queen-raida-social-agent`, `public-social-output-sanitizer`, `x-developer-api`, `discord-send` | `rg-content-strategy` -> `rg-brand-voice` -> `rg-public-output-safety` -> `rg-publishing-ops` | merge | Merged into `workflows/queen-raida-social-publish` campaign mode. |
| `queen-raida-x-response-draft-review-publish` | 5 | Queen Raida social publish | `queen-raida-social-agent`, `x-developer-api`, `public-social-output-sanitizer`, `prism-api-reader`, `prism-api-writer`, `change-request-ops` | `rg-content-strategy` -> `rg-brand-voice` -> `rg-public-output-safety` -> `rg-publishing-ops` | keep-canonical | Base for `workflows/queen-raida-social-publish`. |
| `queen-raida-x-follow-scout-review-follow` | 1 | Queen Raida social graph ops | `queen-raida-social-agent`, `x-developer-api`, `prism-api-reader`, `prism-api-writer`, `change-request-ops`, `portal-memory-publisher` | `rg-content-strategy` -> `rg-brand-voice` -> `rg-publishing-ops` plus future social-graph reference | workflow-reference | Implemented as `workflows/queen-raida-social-graph-ops`. |
| `monthly-share-distro-proposal` | 6 | DAO/share distro | `prism-api-reader`, `moloch-dao-ops`, `cookiejar-activity-reader` | `rg-dao-ops` -> `rg-publishing-ops` | keep-canonical | Implemented as `workflows/dao-share-distro-proposal`. |
| `crm-document-ingest-enrich` | 3 | CRM document ingest | `change-request-ops` | `rg-crm-ops` | keep-canonical | Implemented as `workflows/crm-document-ingest`. |
| `portal-session-recording-complete` | 4 | Portal session artifact ingest | `prism-api-reader`, `portal-memory-publisher` | `rg-portal-ops` | keep-canonical | Implemented as `workflows/portal-session-recording-complete`. |
| `weekly-portal-activity-snapshot` | 1 | Portal/arcade/activity reporting | `prism-api-reader`, `prism-api-writer`, `discord-send` | `rg-portal-ops` -> `rg-content-strategy` -> `rg-public-output-safety` -> `rg-publishing-ops` | workflow-reference | Implemented as `workflows/portal-activity-report`; absorbs arcade report behavior as a reporting mode. |
| `meeting-transcript-memory-ingest` | 1 | memory ingest | `change-request-ops`, `prism-api-writer` | Prism built-ins `change-request-ops` + `prism-api-writer` | workflow-reference | Implemented as `workflows/meeting-transcript-memory-ingest`; no portable skill needed. |

## Likely Duplicate Families

### Blog / Editorial Publish

Candidates: `blog-post-draft-review-publish`, `blog-post-steered-draft-review-publish`, `fireside-blog-post-draft-publish`, `lore-entry-draft-review-publish`.

Recommendation: keep one canonical blog/editorial publish workflow with source modes: generic, steered, fireside, lore.

### Brief / Podcast / Media

Candidates: `daily-memory-brief-review`, `weekly-public-brief-podcast-publish`, `internal-daily-brief-podcast-publish`, `fireside-recap-video-publish`.

Recommendation: keep public weekly as canonical media workflow in `workflows/brief-media-publish`; keep internal/member-only and fireside recap as visibility/source modes.

### Queen Raida Social

Candidates: `queen-raida-portal-launch-campaign`, `queen-raida-x-response-draft-review-publish`, `queen-raida-x-follow-scout-review-follow`, `publish-queen-raida-article`.

Recommendation: keep X response draft/review/publish as canonical social publish recipe in `workflows/queen-raida-social-publish`; treat launch campaign as campaign mode and follow scout as social graph ops.

### Portal Activity / Reporting

Candidates: `weekly-portal-activity-snapshot` and Portal Arcade reporting source.

Recommendation: keep as workflow recipes. Do not create a standalone reporting skill until several report workflows share stable mechanics.
