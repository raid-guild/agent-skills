Submit the prepared Remotion render job.

Read remotion-input.json and POST it to:
https://remotion-service-production.up.railway.app/render-async

The body must include:
- composition: FiresideRecapScene
- outputKey: firesides/<safe-session-slug>-recap.mp4
- props matching the discovered FiresideRecapScene schema

Create render-attempt.json with request body hash, endpoint, HTTP status, response body, job id if returned, observed state, and timestamp.

If the response is immediately terminal completed, also create render-receipt.json with output URL. Otherwise proceed to render-status-check. If the render API rejects the request, create render-blocker.md and stop with the raw error body.
