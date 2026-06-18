# Remotion Compositions

Use the live Remotion service as source of truth.

## Live Checks

Before changing render assumptions:

- `GET /compositions`
- inspect each composition id/name
- read `schemaUrl` when available
- fetch the schema before regenerating input for a different scene

## Rules

- Do not assume a scene exists from old workflow text.
- Do not assume scene payloads are interchangeable.
- If schema is available, validate against schema before render retry.

## Report

Include:

- available compositions
- chosen composition
- schema URL
- schema/payload mismatch
- missing required props
