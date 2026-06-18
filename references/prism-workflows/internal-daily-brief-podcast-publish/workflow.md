# Internal Daily Brief Podcast Publish

This workflow creates an internal-only daily brief for members, expands the date window when a single day is too sparse, generates a podcast-style audio/video package through the Remotion flow, and publishes the approved result into the Portal CMS with member-only visibility semantics.

## Requested Skills

This workflow should use:
- `prism-api-reader`
- `portal-memory-publisher`
- `remotion-composition-checker`
- `workflow-audio-bucket-uploader`

Use the bucket uploader skill whenever the renderer needs fetchable remote audio URLs.

## Long-Running Render Check

Because video render is a long-running external job, this workflow separates render kickoff from render-status verification. After `video-render` starts or reconciles a job, a human-triggered checkpoint step should be used to re-check job status until a verifiable terminal result exists. Do not treat an unknown or still-running render as ready for final review.
