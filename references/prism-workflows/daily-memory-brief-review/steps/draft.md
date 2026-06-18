# Draft

Create a concise daily brief from Prism Memory for the current weekday or current day context. Use prism-api-reader and prefer the narrowest retrieval path that supports a useful summary.

## Retrieval Guidance

Start with today. If today does not contain enough meaningful member-facing signal, expand the window to the last few days and include relevant recent meeting summaries or meeting-derived artifacts. Use recent meeting context to fill important gaps, not to pad the brief.

## Member-Relevance Filter

Only include updates a community member would reasonably care about, such as:

- notable project or product progress
- community decisions, proposals, or votes
- upcoming events, opportunities, or calls to action
- meaningful publishing, launch, or collaboration updates
- blockers or changes that affect member participation

Do not include low-signal internal or meta items that are not useful to members, such as system reminders, background agent state, infrastructure chatter, or generic knowledge entries with no member-facing impact. For example, a note like "Codex is listening" should be excluded unless it materially changes member experience.

## Output

Return:

- the brief text
- a short source summary with dates, buckets, docs, meeting artifacts, or artifact ids used
- the exact time window used if you had to expand beyond today
- any obvious uncertainty or missing context

Keep the brief selective. If there is very little real signal, return a short brief rather than stretching weak material into a long one.

Do not ask follow-up questions during scheduled or automated runs.
