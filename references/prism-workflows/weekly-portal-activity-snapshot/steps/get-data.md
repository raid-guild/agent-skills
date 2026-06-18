# Get Data

Outcome: collect current Portal CMS activity data and save it as a durable JSON artifact named `portal-activity-data.json`.

Use PAYLOAD_CMS_BASE_URL, PAYLOAD_CMS_EMAIL, and PAYLOAD_CMS_PASSWORD. Use Node fetch if curl is unavailable. Authenticate with POST /api/users/login and Authorization: JWT <token>.

Report windows:

- Current UTC generated_at timestamp.
- Last 7 days.
- Last 30 days.

Query these collections when available: users, profiles, posts, projects, events, inquiries, comments, feedback-submissions. Use limit=0&depth=0 for counts. For each collection capture totalDocs, created in last 7 days, and created in last 30 days using createdAt greater_than filters.

For Feedback Submissions, also fetch new records created in the last 7 days with a modest limit such as limit=25&depth=0, sorted newest first. Try collection slug `feedback-submissions` first and then `feedbackSubmissions`. Do not fail the whole step if the feedback collection is unavailable; record feedback as unavailable.

Also retrieve the latest prior Portal activity snapshot from Prism Memory/artifacts when available by listing memory artifacts with source `portal-cms`, type `portal_activity_snapshot`, limit 100, or by searching memory for source `portal-cms` and type `portal_activity_snapshot`. Choose the latest prior snapshot before the current run.

The JSON artifact should include task_key, generated_at, windows, metrics, feedback_records, prior_snapshot_id or null, and prior_snapshot_summary when available.
