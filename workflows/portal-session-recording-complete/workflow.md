# Portal Session Recording Complete

This workflow handles recording-complete events for Portal sessions.

It ingests recording artifacts, verifies Portal resources, plans the next occurrence for recurring sessions, and applies recurrence updates only when appropriate.

The live Portal write steps use `rg-portal-ops`. The recurrence application step has `autoRun: false` because it can create or alter future session records.
