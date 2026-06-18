---
name: rg-public-output-safety
description: Use before publishing, queueing, sending, or presenting any RaidGuild public or community-facing output for X, Discord, Portal/CMS, blogs, newsletters, announcements, sales collateral, Queen Raida posts, AI Solutions copy, or public briefs. Reviews drafts for secrets, credentials, private client/member context, internal URLs, local paths, unsupported claims, confusing agent/debug language, persona/account mismatch, approval gaps, and human-review blockers. Returns sanitized text, changes, and blockers.
---

# RaidGuild Public Output Safety

Use this skill as the final safety gate for public or community-facing output.

This skill owns redaction, blocker detection, public-claim discipline, and persona/account safety. It does not own brand voice, content strategy, research, or publishing mechanics.

## Use Before

- X posts, replies, quotes, and queued drafts
- Discord public/community messages
- Portal/CMS public posts, pages, briefs, and wiki content
- newsletters, public announcements, launch notes, and sales collateral
- Queen Raida or other agent persona output
- generated captions, scripts, summaries, or snippets that may become public

## Routing

Read references as needed:

- Risk patterns: `references/public-risk-patterns.md`
- Required JSON output contract: `references/output-json-contract.md`

If the draft has voice problems but no safety issue, note it and recommend `rg-brand-voice`.

If the draft lacks source support, block or mark `needs_source`; do not invent replacement facts.

If the user asks to publish/send after sanitization, this skill still does not perform the publish action. Route to the relevant ops skill only after safety blockers are resolved and approval is explicit.

## Review Areas

Check for:

1. Secrets, credentials, tokens, keys, cookies, signed URLs, auth headers, database URLs, or env var values.
2. Internal URLs, localhost, private admin routes, raw API routes, service-token artifact URLs, and non-public recording links.
3. Local paths, runtime paths, stack traces, command logs, checkpoint files, and implementation-only artifact paths.
4. Private client, contributor, Discord, meeting, governance, financial, or operational notes.
5. Unsupported claims about dates, prices, availability, partnerships, clients, funding, governance outcomes, member roles, project status, cohort admissions, legal/financial statements, or performance guarantees.
6. Confusing agent/debug language such as tool traces, workflow steps, artifact ids, system prompts, raw JSON, logs, and "as an AI" phrasing.
7. Persona/account mismatch, especially Queen Raida / `@raidguildish` speaking as `@RaidGuild` HQ, implying human membership, or claiming governance authority.
8. Missing human approval for public, client-sensitive, financial, governance, or security-sensitive output.

## Sanitization Rules

- Preserve intent when safe.
- Prefer minimal edits.
- Replace secrets with `[REDACTED_SECRET]`.
- Replace unsafe internal links with `[redacted internal URL]` unless a public URL is provided.
- Remove private operational detail rather than hinting at it.
- If safe rewriting would change the meaning, return the safest text and add a blocker.
- High or critical blockers mean do not publish.

## Output

Return exactly the JSON shape defined in `references/output-json-contract.md`. Do not add prose outside the JSON.
