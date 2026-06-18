# Portal Draft Or Publish

Operator-started agent node (`autoRun: false`).

Use `rg-portal-ops`.

Before writing:

- confirm the operator wants this step to run
- verify Portal target environment
- verify draft vs live publish expectation
- verify visibility
- verify approved package and safety result

Create or update the Portal post.

Create `publish-receipt.json` with:

- Portal post id
- slug
- draft/live status
- admin URL or public URL when available
- media ids or artifact refs
- inline image handling result
- source object links
- any validation warnings

If credentials, schema conversion, media upload, or rich text validation fail, stop with a clear blocker instead of partially publishing as if complete.
