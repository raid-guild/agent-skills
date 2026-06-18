# Draft Discord Review

Prepare and send the share distro review message for Discord channel `#so-dev` using channel ID `1374448934436733089`.

## Destination

Send the live review message only to the RaidGuild Discord #so-dev channel.

- Guild ID: `684227450204323876`
- Channel ID: `1374448934436733089`
- Channel label: `#so-dev`

Use the numeric channel ID as the source of truth. Do not choose a destination by channel name or label alone. Do not post to channel `1511003703090610359`; that channel was used by mistake for request #149.

When attaching the Discord external ref, include the numeric channel ID and guild ID in metadata so checkpoints can verify the destination. If a prior message exists in any other channel, do not treat it as the live review message; create or reconcile the review message in channel `1374448934436733089`.

## Required artifact

Write `discord-draft.md`.

The draft should include:

- cycle key and date window, not just month covered
- source artifact used, such as `docs/participation-steward/aprmay2026.md`
- short summary of evidence sources used
- number of recipients
- total cycle gains or shares to mint
- links or names of key artifacts to review
- any open identity or scoring caveats

## Per-member breakdown

Include a detailed but readable breakdown of how people earned shares.

For each member, include when available:

- display name
- wallet or Discord handle for disambiguation
- total cycle gains
- Engagement score and evidence
- Stewardship score and evidence
- Contribution score and evidence
- short notes when a score depends on manual confirmation, identity resolution, or audit caveat

Do not describe the distro in old Raid / RIP / CookieJar / Meeting lanes unless this is explicitly a historical monthly rerun.

Prefer a compact table or bullet list that reviewers can scan in Discord without opening the JSON first.

## Delivery rules

- Post the report to Discord in this step so review happens against the same message humans will inspect.
- Treat this Discord post as the workflow's review-phase share distro report.
- If the workflow already has a live Discord message for this request, reconcile it instead of posting duplicates when possible.
- Attach a Discord external ref for the live review message when one is created.

Do not wait for a later workflow step to send the review report.
