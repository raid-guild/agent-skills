# Render Checkpoint

Checkpoint node. Wait for the render job to complete, fail, or require operator intervention.

On resume, use `rg-media-render-ops` to check the render job from `render-job.md`.

Route onward only when:

- the render completed and output URL/artifact is available
- the job failed and failure details are captured for review
- the operator confirms a manually completed render artifact

Produce `render-status.md` with final status, output URLs, logs or error summary, and retry recommendation.
