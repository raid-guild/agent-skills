# Audio Render Inputs

External renderers need fetchable audio URLs.

## Rules

- Do not use service-token-only workflow artifact URLs in render payloads.
- Upload approved audio artifacts through `s3-object-storage` when needed.
- Each `props.segments[].url` must be an absolute URL fetchable by the renderer.
- Each segment needs positive `durationMs`.
- Preserve the uploaded URL/object key in `render-plan.json`.

## Evidence

Record:

- source artifact
- uploaded URL
- object key
- segment order
- duration
- speaker/color metadata if used

If upload or URL generation fails, fail before render submission.
