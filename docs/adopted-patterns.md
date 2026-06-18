# Adopted Skill Patterns

This repo borrows several useful patterns from Samber's `cc-skills` project, especially the copywriting and progressive-disclosure skills.

Source references:

- `https://github.com/samber/cc-skills`
- `https://github.com/samber/cc-skills/blob/main/skills/copywriting-prose-creator/references/anti-patterns.md`

## Patterns To Adopt

### 1. Separate Creation, Operation, And Audit

Avoid one skill that both creates strategy, writes copy, audits quality, and publishes output.

Use separate modes or separate skills:

- `BUILD`: create a guide, strategy, campaign structure, or reusable artifact.
- `ADAPT`: transform an existing artifact for a channel, audience, persona, or format.
- `AUDIT`: evaluate existing output against a rubric, source discipline, voice guide, or safety policy.
- `OPERATE`: call APIs, update systems, publish, reconcile, or perform live tool work.

For RaidGuild, this means `rg-brand-voice` and `rg-content-strategy` can draft or evaluate, while `rg-publishing-ops` handles queueing, sending, scheduling, and live URL reconciliation.

### 2. Keep Anti-Patterns In References

Do not bury long banned-word lists, AI tells, punctuation policies, and opener inventories in `SKILL.md`.

Put them in focused references such as:

```text
skills/rg-brand-voice/references/language-anti-patterns.md
skills/rg-content-strategy/references/editorial-anti-patterns.md
skills/rg-public-output-safety/references/public-risk-patterns.md
```

The main skill should route to the relevant reference only when doing an audit, final polish, or guide creation task.

### 3. Make Skills Declare What They Are Not For

Useful descriptions say both when to use the skill and when not to use it. This reduces trigger collisions.

Example boundary:

```text
rg-brand-voice:
Use for voice, prose mechanics, tone, persona fit, language anti-patterns, and copy polish.
Not for publishing, queueing, API calls, calendar updates, source research, or live system operations.
```

### 4. Use Channel Groups Instead Of Platform Explosion

Prefer broad channel groups:

- short social
- long-form editorial
- Discord/community updates
- newsletters/email
- website/landing pages
- sales/collateral
- scripts/media

Put platform-specific details in references only when the difference changes behavior.

### 5. Prefer Falsifiable Style Rules

Avoid vague instructions like "make it more human" or "sound on brand."

Use testable rules:

- no unsupported client, date, outcome, partnership, governance, or funding claims
- one concrete detail before any abstract claim
- no generic AI/corporate openers
- no unexplained operational jargon in public copy
- lore texture must not obscure the factual point
- avoid repeated three-part lists unless the rhythm earns it

### 6. Treat AI Detection As Triage

Do not claim something is AI-generated based on one signal such as punctuation or a single word. Use anti-pattern checks as editorial triage, then rewrite concrete issues.

### 7. Keep Workflow Recipes Out Of Published Skills

A workflow can compose several skills, but it should not automatically become a skill.

For each Prism workflow, extract:

- reusable capability guidance into skills
- live system details into ops references
- one-off sequencing into workflow references
- persona/campaign material into brand/content references

## Patterns To Avoid

- Copying a whole legacy Prism skill into a new `SKILL.md`.
- Making one skill per persona, campaign, or recurring report.
- Duplicating public safety rules in every publishing or writing skill.
- Putting API endpoints inside brand/content skills.
- Putting brand voice rules inside publishing ops skills.
- Letting anti-pattern lists become static forever; review them periodically as model defaults change.
