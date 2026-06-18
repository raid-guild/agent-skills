# Weekly Public Brief Podcast Publish

This workflow creates a public-safe weekly brief, generates podcast audio, prepares a Remotion scene payload, renders media, routes through human review, and publishes the approved result.

## Purpose

Use this workflow for a weekly public brief that should end with:
- a public-safe written brief
- a two-host podcast script
- TTS audio segments
- a canonical Remotion input artifact
- a render receipt for the chosen media output
- a publish receipt for the final CMS write

## High-Level Flow

1. `period-intake`
   Resolve the weekly time window, audience, safety constraints, and source set.
2. `public-summary`
   Produce a public-safe weekly summary and supporting artifact.
3. `podcast-script`
   Produce the two-host script and structured segment data.
4. `review`
   Human gate for editorial approval before media generation.
5. `tts-render`
   Generate audio artifacts and a durable TTS manifest.
6. `remotion-prep`
   Build the canonical Remotion payload and render plan artifacts.
7. `video-render`
   Render or reconcile the media job and write render attempt / render receipt artifacts.
8. `final-review`
   Human gate for whether the chosen render should be published.
9. `publish`
   Publish the approved brief and write a publish receipt.
10. `closed`
   Workflow is complete.

## Human Gates

This workflow depends on two human decisions:
- editorial approval before media generation
- final approval before publish

The workflow cares about the domain truth of those gates:
- was there an approval
- was there a request for changes
- was there a rejection

Platform-level request status projection, current-step projection, auto-continue behavior, and terminal-state handling are owned by the workflow engine, not by these files.

## Artifact Contracts

Later steps must rely on request artifacts, not chat text.

Expected durable artifacts:
- `weekly-summary.md` and `weekly-summary.json`
- `podcast-script.md` and `podcast-script.json`
- `tts-manifest.json`
- segment MP3 artifacts
- `remotion-input.json`
- `render-plan.json`
- `render-attempt.json` when a render job is started but not yet completed
- `render-receipt.json` for completed or terminal render outcomes
- `publish-receipt.json`

## Render Truth

Render retries must be resumable.

If a render job has already been started for the latest `remotion-input.json`:
- reuse the existing job if it is still running
- reconcile its status before starting a duplicate job
- only start a new render when the existing attempt is terminal or a human explicitly requests a fresh rerun

The workflow should preserve domain evidence:
- which payload was rendered
- which render job id corresponds to that payload
- whether the latest attempt is pending, completed, or failed
- which receipt is the last confirmed successful render

## Publish Truth

The publish step should determine:
- whether there was an explicit publish approval
- which completed render receipt is being used
- which media URL was chosen
- whether publishing used the newest successful render or an explicitly accepted fallback

## Durable State

Workflow runtime state belongs in DB-backed request/workflow records, not markdown files.

These files define process, evidence, and artifact expectations. They do not define request status projection, current step, retry counters, run history, or terminal-state semantics.

## Long-Running Render Check

Because video render is a long-running external job, this workflow separates render kickoff from render-status verification. After `video-render` starts or reconciles a job, a human-triggered checkpoint step should be used to re-check job status until a verifiable terminal result exists. Do not treat an unknown or still-running render as ready for final review.

## Public Positioning

This workflow should produce a public-safe peek into guild operations that makes RaidGuild feel active, dynamic, and worth following without exposing client detail, private strategy, or sensitive internal context.

The public brief should help a reader understand that work is happening, projects are moving, and there are real ways to get involved. It should not read like an internal transcript dump.

The public-facing output should usually include a concise call to action that points readers toward the Portal to follow along, see active projects, join upcoming sessions, and plug into real opportunities across RaidGuild.
