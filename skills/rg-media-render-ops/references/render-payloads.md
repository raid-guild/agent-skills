# Render Payloads

Use this for `remotion-input.json` and `render-plan.json`.

## DarkFactoryScene Contract

Current known live schema expects:

- top-level `composition`
- optional `outputKey`
- `props.segments` as non-empty array
- each segment:
  - `url` required
  - `durationMs` required and positive
  - `speaker` optional
  - `color` optional

Do not send `waveform`; the service generates it.

## Rules

- Keep render plan and input in sync.
- Validate URLs before render.
- Validate durations before render.
- Preserve composition-specific props.
- If output is too short or visually wrong, suspect payload shape before assuming renderer success.
