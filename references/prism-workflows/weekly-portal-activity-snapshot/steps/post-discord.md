# Post To Discord

Outcome: send `portal-activity-report.md` to Discord channel #so-dev.

Destination:

- Channel name: #so-dev
- Channel ID: 1374448934436733089

Use the discord-send skill or communication adapter. Send only the concise Discord-ready report from the report artifact. Do not include internal debug notes, local paths, secrets, private contact details from feedback submissions, or raw JSON unless it is already part of the concise report.

After sending, attach a Discord external ref to the request with provider `discord`, kind `message`, the message id if available, URL if available, state `sent`, and metadata containing channelId `1374448934436733089` and channelName `so-dev`.
