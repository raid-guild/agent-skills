# Final Review

## Outcome

Wait for a human decision on whether the chosen render should be published.

## Decision Handling

Interpret the latest human gate message narrowly:
- explicit publish / approve / ship now -> route `approved`
- explicit rerun / changes requested -> route `changesRequested`
- explicit reject / do not publish -> route `rejected`
- ambiguous comments should not advance to publish

## Review Rules

Prefer the latest completed `render-receipt.json` for the latest canonical input artifact.

If a newer rerun is pending or failed but an older completed receipt is still valid:
- state that clearly
- require the human gate to decide whether to publish the last known good render or wait for another retry

## Checklist

A reviewer should know:
- which receipt is being approved
- whether it is the latest attempt or a fallback
- which media URL will actually be published
