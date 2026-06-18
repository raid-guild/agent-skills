# Steering

Human gate. Confirm the request is scoped to a brief, podcast, or recap media publish workflow.

Approve only when the request identifies enough of:

- source mode: `weekly_public`, `internal_daily`, `daily_memory`, `fireside_recap`, or `brief_only`
- time window, session, source pack, or Prism Memory digest
- visibility: public, member/internal, draft-only, or authenticated-only
- desired outputs: written brief, podcast script, audio, video, Portal draft, Discord summary, X draft
- target destination, if known
- whether generated media is required

Route:

- `approved` -> `source-intake`
- `changesRequested` -> `steering`
- `rejected` -> `closed`
