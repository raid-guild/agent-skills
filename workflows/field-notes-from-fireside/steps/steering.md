# Steering

Human gate. Confirm the request is scoped to a completed or source-ready Fireside session.

Approve only when enough of the following is identified:

- Portal session/event id or URL
- transcript, summary, recording, or source artifact links
- desired outputs: source pack, topic map, media brief, X draft, child requests
- whether blog, wiki, and recap media child requests should all be created
- any known guest, host, theme, title, or session constraints

Route:

- `approved` -> `session-intake`
- `changesRequested` -> `steering`
- `rejected` -> `closed`
