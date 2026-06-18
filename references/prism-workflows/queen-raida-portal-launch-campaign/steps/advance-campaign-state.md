# Advance Campaign State

Update campaign state after successful publishing.

Read `campaign-state.json` and `publish-receipt.json`. Increment `currentIndex`, set `lastTweetId`, set `lastPostedAt`, and mark campaign `completed` if the final post slot has been published.

Save the updated `campaign-state.json` as a request artifact. Return the new state and next scheduled phase.
