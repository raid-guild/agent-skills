# Weekly Portal Activity Snapshot

This workflow creates the weekly Portal CMS activity snapshot from live Portal CMS data, stores the report in Prism Memory, and posts a concise Discord-ready report to #so-dev.

The workflow is intended to be started by the scheduled task `weekly-portal-activity-snapshot`. It does not mutate Portal CMS and does not create unrelated change requests.

Durable outputs:

- `portal-activity-data.json` from Get Data.
- `portal-activity-report.md` from Create Report.
- A Prism Memory inbox item with source `portal-cms`, bucket `portal`, type `portal_activity_snapshot`.
- A Discord message external ref after posting to #so-dev.
