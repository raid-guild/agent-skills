# Create Report

Outcome: create a concise weekly report from `portal-activity-data.json`, store it as `portal-activity-report.md`, and write the snapshot to Prism Memory.

Compare current totals and window counts against the prior snapshot when available. Report deltas for users/signups, profiles, posts, projects, events, inquiries, comments, and feedback submissions. If no prior snapshot exists, state that this is the baseline.

Add a distinct section titled `User Feedback`. Summarize new Feedback Submissions records from the last 7 days, including count, recurring themes, notable requests or issues, sentiment when inferable, and urgent follow-up items. Keep feedback summaries concise and avoid exposing private contact details. Refer to submitters generically unless the record is clearly intended as public attribution.

Store the new snapshot as a Prism Memory inbox item with source `portal-cms`, bucket `portal`, type `portal_activity_snapshot`, author `weekly-portal-activity-snapshot`. Include structured JSON in metadata with task_key, generated_at, windows, metrics, feedback_summary, prior_snapshot_id or null, and deltas. Content should include the human-readable summary plus the structured JSON block.

The report artifact should be Discord-ready and concise.
