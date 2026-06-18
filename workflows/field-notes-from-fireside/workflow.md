# Field Notes From Fireside

This is the orchestration parent for turning a completed Fireside session into a source-backed content package.

It creates:

- source pack
- topic map
- media brief
- Portal session artifact/resource updates
- one Bard Calendar X draft for later review/scheduling
- non-autostart child requests for blog, wiki, and recap media work

It does not:

- publish to X
- create Portal blog post drafts
- create or update Portal wiki pages
- render recap video
- auto-run child content workflows

## Canonical Shape

1. Human steering gate confirms the Portal session, source artifacts, and desired outputs.
2. Session intake verifies the source set.
3. Source pack separates evidence, gaps, and public-safe facts.
4. Topic map separates session reports, broad wiki topics, and narrow blog angles.
5. Media brief prepares visual and recap direction for downstream media work.
6. Portal artifacts step attaches source/planning resources to the session/event.
7. Human package review approves the package for downstream requests.
8. Calendar draft creates exactly one Bard Calendar X draft or planned event.
9. Spawn child requests creates queued child requests with `autoRun: false`.

## Child Recipes

- `blog-editorial-publish` with `fireside` mode for one focused blog angle.
- `fireside-wiki-topic-develop` for exploratory Portal wiki topic work until a normalized wiki/research recipe exists.
- `brief-media-publish` with `fireside_recap` mode for recap video/media.

## Inquiry Standard

Fireside source work should prefer curiosity over closure. Name gaps, expose uncertainty, and preserve alternatives instead of forcing a confident narrative from partial evidence. Verify Portal/session claims directly or mark them as unknown.
