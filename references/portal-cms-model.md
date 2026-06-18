# Portal CMS Model Reference

This reference supports the exported `portal-ops-skill` instructions. It captures the Portal CMS primitives the skill is expected to reason about when planning or writing source-grounded Portal updates.

## Core Collections

| Collection | Purpose | Common Fields | Notes |
| --- | --- | --- | --- |
| `activityItems` | Factual dated signals: decisions, blockers, launches, contributions, updates, or evidence-backed observations. | `title`, `summary`, `occurredAt`, `sourceUrl`, `relatedProjects`, `relatedThreads`, `relatedEvents`, `relatedProfiles` | Prefer these for discrete facts rather than ongoing narrative. |
| `threads` | Ongoing lines of work, thought, or coordination. | `title`, `summary`, `status`, `relatedProjects`, `relatedActivityItems`, `relatedProfiles` | Threads are continuity records, not task boards or categories. |
| `events` | Sessions, meetings, calendar anchors, and recordings. | `title`, `start`, `end`, `description`, `hosts`, `resources`, `artifacts`, `discordEventUrl`, `calendarUrl` | Use the dedicated event create/sync routes when Discord/calendar sync is required. |
| `projects` | Live collaboration surfaces with people, links, state, and next actions. | `title`, `summary`, `status`, `links`, `members`, `relatedThreads`, `relatedActivityItems` | Create only when there is a concrete collaboration surface. |
| `dailyBriefs` | Assembled current snapshot across activity, threads, projects, events, and engagement actions. | `date`, `summary`, `sections`, `relatedActivityItems`, `relatedThreads`, `relatedProjects` | Briefs summarize sourced Portal state; they should not invent facts. |
| `profiles` | People and contributor records. | `name`, `handle`, `bio`, `links`, `roles`, `avatar` | Preserve uncertainty for identity or role claims. |
| `spotlights` | Admin/editorial placement for featured Portal content. | `title`, `summary`, `target`, `startsAt`, `endsAt`, `priority` | Use only for intentional editorial emphasis. |
| `wikiPages` | Durable source-backed topic pages and living knowledge maps. | `title`, `slug`, `summary`, `body`, `sources`, `sourceSessions`, `relatedPages` | Use for evergreen knowledge, not transient status updates. |

## Modeling Rules

- Preserve source provenance in `sourceUrl`, `sources`, artifacts, or related records.
- Update existing projects, threads, events, and wiki pages before creating duplicates.
- Keep projects as collaboration surfaces and threads as continuity records.
- Keep sessions practical: time, join/calendar links, hosts, resources, recordings, and artifacts.
- Draft instead of publishing when timestamps, participants, source URLs, or permissions are unclear.
- Do not expose private IDs, raw tokens, hidden admin routes, or local runtime paths in public Portal copy.
