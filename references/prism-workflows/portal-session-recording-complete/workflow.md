# Portal Session Recording Complete

This workflow handles Discord recording-complete events for Portal session records.

Portal owns event records and authenticated APIs. Prism owns hook orchestration, normalized intermediate artifacts, idempotency checks, and final structured logging.

## Workflow Shape

1. Intake: normalize hook payload into `portal-session-intake.json`.
2. Ingest Artifacts: call Portal artifact ingest only when intake has a reliable match; write `portal-session-artifact-ingest.json`.
3. Plan Next Occurrence: create a recurrence decision artifact; write `portal-session-next-occurrence-plan.json`.
4. Apply Next Occurrence: perform any required Portal recurrence mutation and write the single final `portal-session-recording-complete-result.json`.
5. Closed.

Earlier steps must not write final result artifacts. Downstream steps must be safe no-ops when upstream status is noop/failed, because the workflow engine may continue through the linear step chain.
