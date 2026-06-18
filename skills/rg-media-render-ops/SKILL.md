---
name: rg-media-render-ops
description: Use when Codex needs to inspect, validate, repair, or diagnose RaidGuild media rendering workflows, including Remotion renderer composition discovery, schema validation, render payload shape, audio segment URL readiness, TTS/audio artifact preparation, render-plan/remotion-input reconciliation, render failure diagnosis, and deciding whether to rerun prep or render steps. Use s3-object-storage for generic uploads and fetchable URLs.
---

# RaidGuild Media Render Ops

Use this skill for media/render pipeline mechanics.

This skill owns Remotion composition checks, render payload validation, media input readiness, and render failure diagnosis. It does not own generic object storage; route uploads to `s3-object-storage`.

## Routing

Read only the references needed:

- Remotion composition checks: `references/remotion-compositions.md`
- Render payloads: `references/render-payloads.md`
- Audio render inputs: `references/audio-render-inputs.md`
- Failure recovery: `references/failure-recovery.md`

Use `s3-object-storage` when workflow artifacts need S3-compatible upload or durable fetchable URLs.

## Operating Rules

- Use the live renderer as source of truth for available compositions and schemas.
- Do not assume a composition exists because an old workflow named it.
- Do not assume two scenes accept the same payload shape.
- Do not point external renderers at service-token-only artifact URLs.
- If render output succeeds but is obviously wrong, treat it as a payload or asset mismatch until proven otherwise.
- Preserve render inputs and plans as durable artifacts for reconciliation.

## Workflow

1. Inspect available compositions when composition/schema is uncertain.
2. Fetch schema when available.
3. Validate `remotion-input.json` and `render-plan.json`.
4. Ensure all media URLs are fetchable by the renderer.
5. Route private artifact upload needs to `s3-object-storage`.
6. Diagnose failures and decide whether retry starts at prep or render.

## Output

When diagnosing:

- available compositions
- schema URL used
- payload mismatch or uncertainty
- media URL readiness
- retry start point
- required artifact updates
