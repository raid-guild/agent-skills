Checkpoint/polling step for the async Remotion job.

Read latest render-attempt.json and poll the job id using the Remotion async status endpoint, following the existing weekly podcast workflow pattern:
GET https://remotion-service-production.up.railway.app/render-async/<jobId>

Behavior:
- If status is running/queued/processing, refresh render-attempt.json with the latest state and return a concise still-running summary. Do not advance.
- If status is completed/succeeded, create render-receipt.json with job id, output URL, outputKey, duration if available, and verification timestamp. Then advance to final-review.
- If status is failed/error/canceled, create render-blocker.md with the raw status/error body and stop.

This checkpoint exists to wait for render completion before human final review.
