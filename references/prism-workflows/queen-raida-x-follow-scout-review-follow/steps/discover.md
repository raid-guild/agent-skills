# Discover Candidates

Outcome: produce a ranked follow-candidate report for human review. Do not follow anyone in this step.

Use these sources, in this order:

1. Portal CMS profiles when available. Look for X/Twitter handles in contact.x, and tolerate the field being absent while it is rolling out. Also check any existing Twitter/X contact shape if present.
2. Seed accounts: @RaidGuild, @0xSero, @raidguildish, and known RaidGuild members found in Portal CMS.
3. X graph expansion through x-developer-api: followers/following of @RaidGuild, @0xSero, and high-confidence known member handles.
4. X recent search for relevant topics: AI agents, autonomous orgs, DAO tooling, public goods, onchain ops, devtools, creative coding, coordination, agent infrastructure, and builder communities.
5. Prism Knowledge and Prism Memory for recent RaidGuild projects, members, collaborators, and community context.

Candidate scoring:

- known_member: Portal CMS or strong RaidGuild source confirms membership.
- member_adjacent: followed by or interacting with several known members.
- project_collaborator: tied to a RaidGuild project, client-safe public work, or community session.
- external_ai_scene: relevant AI/agent builder with public signal.
- coordination/devtools: relevant to DAO tooling, devtools, public goods, or autonomous orgs.

Risk flags:

- protected/private account
- spam/engagement bait
- mostly politics or rage content
- NSFW/high-risk brand mismatch
- impersonation risk
- no recent relevant posts
- already followed by @raidguildish
- blocked/muted/unavailable if the API exposes that state

Return a markdown report and create a request artifact named follow-candidates.md when request context is available. Include for each candidate: handle, display name, URL, source path, why follow, recent relevant post examples or summaries, score, risk flags, and recommendation: follow / watch / ignore.

Also include machine-readable JSON in the report or a separate follow-candidates.json artifact if artifacts are available.
