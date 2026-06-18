# Failure Recovery

Use this when media render jobs fail or output looks wrong.

## Recovery Pattern

1. Check available compositions.
2. Fetch target schema.
3. Compare schema to `remotion-input.json`.
4. Validate all media URLs are fetchable.
5. Regenerate `remotion-input.json` and `render-plan.json` if needed.
6. Retry from prep when inputs are wrong.
7. Retry render only when inputs are valid and failure is transient.

## Failure Interpretation

- `fetch failed` alone does not prove timeout.
- Generic runtime traces may mean the step failed before structured upstream errors.
- Very short output for a multi-segment brief usually means degenerate payload or fallback scene.
- A successful render with wrong content is not a true success.

## Report

Include:

- failure class
- evidence checked
- corrected artifact paths
- retry point
- whether another approval is needed
