# Follow Approved Accounts

Outcome: follow only the exact human-approved X handles/accounts.

Use x-developer-api. Before following:

1. Verify the authenticated account is @raidguildish unless the request explicitly approves another account.
2. Re-resolve each approved handle to a current X user id.
3. Skip any account already followed.
4. Do not follow accounts not explicitly approved in the review gate.

After following, record results in a Prism memory inbox item with source queen-raida-follow-scout, type x_follow_actions, bucket_hint social, and include followed handles, URLs, source request, skipped accounts, errors, and timestamp.

Attach external refs for followed X profiles when request context is available. Return a concise follow summary.
