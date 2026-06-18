# Media Prep

Use `rg-media-render-ops`, `s3-object-storage`, and `rg-public-output-safety` for public titles/descriptions.

Read `brief-draft.md`, `media-script.md`, and `tts-result.md`.

Prepare the render payload:

- inspect available composition and schema when needed
- map script, audio URLs, title, summary, and scene data to the expected payload
- validate public title/description through the sanitizer when public
- include only fetchable media URLs

Produce `render-payload.json` and `render-prep-notes.md`.
