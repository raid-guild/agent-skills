# Render Status Check

## Outcome

Check the existing render job status for the latest canonical payload and determine whether the workflow can advance to final review.

## Step Type Behavior

This is a human-triggered checkpoint for a long-running external job. Run it whenever an operator wants to re-check the status of the most recent Remotion render without re-submitting the render itself.

## Use This Context

- `render-attempt.json`
- `render-plan.json`
- `remotion-input.json`
- any existing `render-receipt.json`
- relevant request comments or notes about retries

Use `remotion-composition-checker` guidance and the live renderer status surfaces that are actually available.

For full-scene render jobs on this Remotion service, check the canonical async status endpoint first:
- `GET /render-async/<jobId>`

Treat that endpoint as the primary status source for jobs created by `POST /render-async`. Only fall back to broader probe attempts if this canonical route is unavailable in the deployed service.

## Required Behavior

- do not submit a new render from this step
- use the known render job id from `render-attempt.json` when available
- probe the renderer's readable status endpoint for the existing job, starting with `GET /render-async/<jobId>` for full-scene jobs created by `POST /render-async`
- if the job is still queued, running, or unreadable, refresh `render-attempt.json` with the latest evidence and remain in this checkpoint
- if the job is verifiably completed, write a terminal `render-receipt.json` and state that the workflow is ready to move to `final-review`
- if the job is verifiably failed, write a terminal `render-receipt.json` describing the failure and state whether the next human action should be retry via `remotion-prep` / `video-render` or to stop
- if probe routes return 404 or another non-terminal ambiguity, record the exact probe evidence instead of paraphrasing loosely

## Durable Artifacts

Always refresh `render-attempt.json` with:
- checked timestamp
- render job id
- probe routes used
- current observed state
- exact evidence for the state

When terminal, write `render-receipt.json` with at least:
- render job id
- final status
- output URL when completed
- completion or failure timestamp when available
- the exact source of truth used for status
- whether this receipt supersedes an older receipt

## Required Output

Return a concise status verdict:
- `still-running`
- `completed-ready-for-final-review`
- `failed-needs-rerun`
- `unknown-waiting-on-better-status-signal`

If the verdict is ready, state explicitly that the next step should be `final-review`. Otherwise explain why the workflow should remain on this checkpoint.
