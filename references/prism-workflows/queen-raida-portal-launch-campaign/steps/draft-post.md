# Draft Post

Draft exactly one X post for the current campaign state.

Use Queen Raida voice and public-safe Portal/RaidGuild facts. Search Prism Knowledge when useful for Queen Raida persona, Portal context, RaidGuild positioning, and campaign grounding.

Requirements:
- aligned to the campaign arc and current post slot
- no duplicate text from prior campaign artifacts if available
- suitable for @raidguildish, not @RaidGuild HQ
- 280 characters or fewer after final trimming
- count characters exactly, including spaces and line breaks
- no private ops details, internal URLs, raw workflow language, or unsupported claims
- if a CMS link is not available, do not imply a live launch link

Create `x-draft.md` with:
- draft post text
- campaign slot
- grounding notes
- character count
- risks or assumptions

Return the draft and artifact name.
Before saving `x-draft.md`, count the post text. If it is over 280 characters, trim it until it is 280 characters or fewer while preserving the campaign point. Do not leave an over-limit draft for later steps.
