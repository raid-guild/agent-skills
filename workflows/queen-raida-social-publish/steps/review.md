# Human Review

Human gate. The operator reviews the exact sanitized public text, target account, target action, destination, and publish mode.

Publishing must not proceed unless the review approval includes:

- approved final text
- approved target account
- approved target action
- approved destination or reply target, when applicable
- queue-only versus publish-now decision

Route:

- `approved` -> `publish`
- `changesRequested` -> `revise`
- `rejected` -> `closed`
