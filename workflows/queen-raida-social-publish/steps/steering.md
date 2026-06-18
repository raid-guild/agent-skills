# Steering

Human gate. Confirm the workflow is scoped to Queen Raida public social output.

Approve only when the request identifies enough of:

- source material or source pack
- source mode: `response`, `new_post`, `thread`, `campaign`, `support`, or `announcement`
- target account, normally `@raidguildish`
- target action: reply, quote, new post, thread, queue draft, or Discord summary
- destination or source URLs when publishing/replying to a specific item
- whether the operator wants direct publish after review or queue-only prep

Route:

- `approved` -> `intake`
- `changesRequested` -> `steering`
- `rejected` -> `closed`
