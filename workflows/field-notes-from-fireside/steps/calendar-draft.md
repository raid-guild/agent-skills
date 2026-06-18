# Calendar X Draft

Use `rg-publishing-ops` and `rg-public-output-safety`.

Create exactly one X draft or planned Bard Calendar item for later human review/scheduling.

Rules:

- target channel defaults to `x: main account`
- do not publish to X
- do not create more than one X draft unless explicitly requested
- inspect upcoming calendar events before creating a new slot
- reuse a fitting existing planned event when available
- record scheduling rationale
- run the public sanitizer before storing the draft

Produce `bard-calendar-x-draft-result.json` with calendar topic id, draft id, event id if assigned, status, planned channel, planned publish time if any, reused-vs-created status, schedule rationale, draft text, source refs, and sanitizer result.
