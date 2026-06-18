# Spawn Child Requests

Use `rg-publishing-ops` for request/calendar coordination if available. Use the local request system configured by the Prism instance when creating child requests.

This agent node has `autoRun: false`. Continue only after the operator approves child request creation.

Create or reconcile non-autostart child requests from the approved Fireside package.

Required child requests:

- `blog-editorial-publish`, mode `fireside`: focused blog post from the strongest approved narrow angle.
- `fireside-wiki-topic-develop`: one or more Portal wiki topic pages from the approved topic map.
- `brief-media-publish`, mode `fireside_recap`: source-grounded recap media using the approved media brief.

Before creating requests, inspect existing refs, comments, and child-request evidence. Reuse existing children instead of creating duplicates.

Set `autoRun: false` on every child request so a human can review/start it later.

Each child description must include:

- parent request id/number
- Portal session/event URL or id
- approved angle/topic
- source pack, topic map, media brief, Bard draft, and Portal artifact links
- instruction to ground all claims in parent artifacts and session sources
- missing inputs or human notes from package review

Produce `spawned-content-requests.json` with one entry per child: workflow key, mode, title, request id/number, URL if available, autoRun, purpose, and reused-vs-created status.
