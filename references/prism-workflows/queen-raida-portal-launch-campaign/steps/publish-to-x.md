# Publish To X

Publish exactly one X post from `sanitized-output.json` using x-developer-api. This workflow is intended to run autonomously, so only publish when `sanitized-output.json` says the post is `publishable`, has no high or critical blockers, and the final post text is 280 characters or fewer.

Attach the selected generated media if the API/tooling supports it. If media upload is unavailable, publish text-only only when the sanitized output explicitly allows text-only fallback; otherwise stop with a clear blocker.

Do not publish if:
- sanitizer marked the output blocked
- a launch/CMS link claim is unsupported
- the configured X account is not @raidguildish
- required media is missing and no text-only fallback is approved
- final post text is over 280 characters

Before calling X, recompute the final post text character count locally, including spaces and line breaks. If the count is over 280, do not call X; write `publish-receipt.json` with status `blocked`, reason `over_280_characters`, and the measured count. Record the X tweet id/url, posted text, final character count, media result, and timestamp in `publish-receipt.json`.

Return the tweet URL and receipt artifact name.
