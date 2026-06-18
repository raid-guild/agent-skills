# Publish Or Queue

Use `rg-publishing-ops` and `rg-public-output-safety`.

This agent node has `autoRun: false`. Continue only after the operator has approved exact text, account, action, and destination.

Before publishing or queuing:

1. Re-run the sanitizer on the exact approved text.
2. Verify the active credentials/account match the approved account, normally `@raidguildish`.
3. Verify the target action matches the approval: reply, quote, new post, thread, queue draft, or Discord summary.
4. Do not alter approved copy except for API-required formatting or operator-approved trimming.
5. If high or critical blockers appear, do not publish; return a blocked result for review.

For queue-only mode, add the approved text to the configured draft queue and capture the queue id.

For publish-now mode, publish only the approved text to the approved destination and capture the posted id and URL.

Produce `queen-raida-social-publish-result.md` with the action taken, final text, account, destination, posted/queued URL or id, sanitizer result, and any API response evidence.
