---
name: public-social-output-sanitizer
description: Use before publishing or presenting draft public output for X, Discord, public CMS/blogs, newsletters, or public announcements. Reviews text for secrets, internal URLs, local paths, private operational notes, unsupported claims, confusing agent/debug language, and account/persona mismatch; returns sanitizedText, changes, and blockers.
---

# Public Social Output Sanitizer

## Purpose

Use this skill before any public social output is posted, queued, or sent for human approval. It is a final safety and clarity pass for public channels.

## Use Before

- X posts or replies
- Discord public/community messages
- public CMS, blog, newsletter, or announcement copy
- generated captions, summaries, or social snippets that may be public

## Required Review Areas

Check the draft for:

1. Secrets or credentials: API keys, bearer tokens, OAuth tokens, private keys, seed phrases, passwords, cookies, service tokens, auth headers, webhook secrets, signed URLs, database URLs, and env var values.
2. Internal URLs: railway.internal, localhost, 127.0.0.1, private service URLs, admin-only routes, service-token artifact URLs, raw API routes, and non-public recording links.
3. Local paths: /app, /data, /tmp, /var, ~/.env, checkpoint files, stack traces, command logs, runtime paths, and implementation-only artifact paths.
4. Private operational notes: hidden workflow instructions, task ids when not public, checkpoints, debug output, rate-limit internals, internal prompts, unreviewed memory snippets, private Discord details, and admin references.
5. Unsupported claims: dates, prices, availability, partnerships, client names, funding, governance outcomes, member roles, project status, cohort admissions, support promises, legal/financial claims, and performance guarantees.
6. Confusing agent/debug language: “I used a tool,” “Prism Memory says,” “artifact id,” “checkpoint,” “workflow step,” “as an AI language model,” “system prompt,” raw JSON, logs, or API route details.
7. Account/persona mismatch: Queen Raida / @raidguildish must not speak as @RaidGuild HQ, imply human membership, claim governance authority, or confuse @raidguildish with the official @RaidGuild account.

## Sanitization Rules

- Preserve intent when safe.
- Prefer minimal edits.
- Do not invent replacement facts.
- Replace secrets with [REDACTED_SECRET].
- Replace unsafe internal links with [redacted internal URL] unless a public URL is provided.
- If safe rewriting would change meaning, keep the safest sanitizedText and add a blocker.
- High or critical blockers mean do not publish.

## Required Output

Return exactly this JSON shape and no extra prose:

```json
{
  "sanitizedText": "",
  "changes": [
    {
      "type": "redaction | rewrite | removal | softening | link_replacement | persona_fix | none",
      "before": "",
      "after": "",
      "reason": ""
    }
  ],
  "blockers": [
    {
      "type": "secret | internal_url | local_path | private_ops | unsupported_claim | confusing_debug_language | persona_mismatch | needs_source | human_review",
      "severity": "low | medium | high | critical",
      "reason": "",
      "suggestedResolution": ""
    }
  ]
}
```

If no changes are needed, return the original draft in sanitizedText, changes as an empty array, and blockers as an empty array.
