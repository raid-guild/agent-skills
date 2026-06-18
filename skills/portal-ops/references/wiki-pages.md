# Wiki Pages

Use `wikiPages` for durable source-backed knowledge pages.

A session can spark a wiki page, but the page should include broader evidence when needed. Do not use wiki pages for simple session recaps, announcements, private notes, or generic SEO content.

## Good Candidates

- technical topic deep dives
- further reading packs
- dated latest-signal briefs
- prompt packs
- research maps
- evergreen practice notes

## Key Fields

- `title`
- `slug`
- `summary`
- `body`
- `sourceSessions`
- `relatedPosts`
- `relatedProjects`
- `relatedThreads`
- `relatedProfiles`
- `relatedActivityItems`
- `keyClaims`
- `furtherReading`
- `papers`
- `tools`
- `openQuestions`
- `prompts`
- `relatedTopics`
- `possibleTopics`
- `sourceArtifacts`
- `reviewStatus`
- `confidence`
- `visibility`
- `_status`

## Review Status

Published wiki pages must have:

```text
reviewStatus: reviewed
```

Use `draft` or `needs_review` for low-confidence, speculative, sensitive, or freshness-dependent pages.

## Workflow

1. Pick one narrow technical or knowledge question.
2. Gather source material from sessions, Prism Memory, official docs, papers, tools, and public sources.
3. Build a claim ledger.
4. Separate facts, opinions, speculation, and open questions.
5. Draft a focused synthesis, not a recap.
6. Attach annotated further reading.
7. Date freshness-sensitive claims.
8. Publish only after review.
