# Steering Gate

Human gate.

Approve only when the request has enough steering to begin agent work.

Required steering:

- source mode: `generic`, `steered`, `fireside`, or `lore`
- topic or source object
- audience
- desired angle or question
- publishing destination and visibility
- source material or retrieval expectations
- constraints, forbidden claims, or privacy notes
- whether media is required, optional, or not wanted
- whether Portal should create a draft only or publish after review

Routes:

- `approved`: continue to `strategy-brief`
- `changesRequested`: stay at `steering`
- `rejected`: close

Do not draft, research, generate media, or create Portal records from this step.
