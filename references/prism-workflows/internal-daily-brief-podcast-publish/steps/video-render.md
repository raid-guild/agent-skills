# Video Render

## Outcome

Start the latest canonical Remotion render job, or reconcile an already-started job without submitting a duplicate render. This step is for kickoff and idempotent reconciliation, not for waiting indefinitely on completion.

## Rules

Assume `remotion-prep` is responsible for producing fetchable remote audio URLs first. If `remotion-input.json` still contains service-token-only artifact URLs or unverified bucket URLs, fail with a concrete explanation instead of attempting a broken render.

## Required Behavior

- if a matching render job already exists for the latest canonical payload, reconcile it instead of creating a duplicate
- if a new render job is submitted, record the returned job id and request metadata immediately
- do not block this step waiting for a long-running render to finish when the renderer has already accepted the job
- if the renderer exposes only partial acknowledgement and no readable terminal status yet, record that clearly instead of inventing success

## Durable Artifacts

Always write or refresh `render-attempt.json` with at least:
- latest canonical input artifact id
- render job id when known
- submission timestamp
- whether the run was newly submitted or reconciled
- current observed state such as `submitted`, `running`, `unknown`, `completed`, or `failed`
- probe routes or APIs used
- concise evidence for the observed state

Write `render-receipt.json` in this step only when the render already has a verifiable terminal result during kickoff or reconciliation. Otherwise leave terminal verification to the render-status checkpoint.
## Remotion Async API

For full-scene renders on this service, the canonical async pattern is:
- start: `POST /render-async`
- poll: `GET /render-async/<jobId>`

Prefer that route pair first for DarkFactoryScene-style jobs before probing any fallback or legacy route guesses.
