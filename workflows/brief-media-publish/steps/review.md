# Content Review

Human gate. Review the written brief and, when present, the media script before generation.

Approval must identify one route:

- `approvedMedia` -> `tts-render`
- `approvedBriefOnly` -> `publish-prep`
- `changesRequested` -> `draft-brief`
- `rejected` -> `closed`

For media runs, do not render audio or video until the script and visibility are approved.
