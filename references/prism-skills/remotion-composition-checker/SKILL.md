---
name: remotion-composition-checker
description: Use this skill when Codex needs to inspect the live Remotion renderer, list available compositions, read composition schemas, validate render payload shape, or diagnose render failures before rerunning remotion-prep or video-render.
---

# Remotion Composition Checker

Use the live Remotion service as source of truth for available compositions and request shape.

## Live Checks

Before changing render assumptions, query the renderer directly:
- `GET /compositions`
- read each composition's `schemaUrl` when available
- fetch the schema before regenerating `remotion-input.json` for a different scene

## Operating Rules

- Do not assume a composition exists because a workflow or prior artifact named it.
- Do not assume two scenes accept the same payload shape.
- If a render succeeds with an obviously wrong output, treat that as a payload-shape failure, not a true success.

## DarkFactoryScene Contract

The live schema currently expects:
- top-level `composition`
- optional `outputKey`
- `props.segments` as a non-empty array
- each segment with:
  - `url` required
  - `durationMs` required
  - `speaker` optional
  - `color` optional
- do not send `waveform`; the service generates it

## Recovery Pattern

When a request used the wrong composition or wrong payload shape:
1. Check `/compositions`.
2. Fetch the target scene's schema.
3. Regenerate the canonical render payload to match the live schema exactly.
4. Save refreshed `remotion-input.json` and `render-plan.json`.
5. Only then rerun `video-render`.

## Failure Interpretation

- `fetch failed` is not enough to prove timeout.
- Missing or generic runtime traces mean the step failed before it produced a structured upstream error.
- A 5-second output for a multi-segment brief usually signals a degenerate or fallback payload shape.

## Output Style

When diagnosing a render issue, report:
- available compositions
- schema URL used
- exact payload mismatch or uncertainty
- whether retry should start at `remotion-prep` or `video-render`
