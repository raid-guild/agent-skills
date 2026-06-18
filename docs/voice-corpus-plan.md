# RaidGuild Voice Corpus Plan

This plan describes how to hone RaidGuild voice without flattening all cultural, operational, and agent-persona material into one generic style.

## Source Types

### 1. Culture Roots

Sources:

- `https://github.com/raid-guild/origin-stories`
- `https://blog.traviswyche.com/p/what-the-fuck-is-raid-guild`

Use for:

- member language
- myth, weirdness, and emotional charge
- why people join, stay, build, and identify with the guild
- what RaidGuild feels like from inside the community

Do not use for:

- operational policy
- client-safe sales copy without moderation
- factual claims unless separately sourced

The Travis post should be treated as high-spice cultural source material. Its metadata points toward a punk/metal/Moloch/coordination-failure/web3 cultural register. That is useful as edge texture, not as the default voice for every output.

### 2. Institutional And Brand System

Sources:

- `https://github.com/raid-guild/handbook-v2`
- `https://x.com/RaidGuild`
- `RG_BRAND_AGENTS.md`
- current brand/design system sources

Use for:

- official terminology
- visual/copy consistency
- brand-safe defaults
- official public social voice
- documentation and site copy constraints
- UI, design, and asset guidance

Do not use for:

- deep cultural weirdness
- member story tone
- Queen Raida persona specificity

The `@RaidGuild` X account should be treated as the official HQ public-social voice source. Keep it separate from Queen Raida's `@raidguildish` persona: `@RaidGuild` can speak as the guild account; Queen Raida can reference RaidGuild but should not impersonate HQ.

### 3. Agent Persona Sources

Sources:

- `https://github.com/raid-guild/Queen-Raida`
- `docs/persona.md`
- `docs/publishing-policy.md`
- `docs/safety-and-sanitizer.md`
- `docs/capability-manifest.md`
- `docs/media-inspiration.md`

Use for:

- Queen Raida voice and boundaries
- agent capability claims
- public publishing policy
- operational-occult texture
- persona/account mismatch checks

Do not use for:

- official RaidGuild HQ voice
- human member voice
- client commitments
- generic RaidGuild brand copy

Queen Raida should remain a persona overlay. The useful rule is: clear operational fact first, weird machinery second.

### 4. Prism Memory

Sources:

- linked Railway Prism Memory instance
- local `prism-memory-kit/prism-memory`
- Prism digests, memory entries, knowledge records, workflow artifacts, and source-backed summaries

Use for:

- recent signals
- source-grounded facts
- live project context
- community activity
- examples of how agents currently describe work
- discovering current terminology, active projects, and recent coordination patterns

Do not use for:

- stable brand doctrine by itself
- private context without approval
- public claims unless the source is public-safe
- permanent voice rules without editorial review
- copying internal memory entries directly into public copy
- treating one recent agent-written digest as canonical style

Prism Memory is a fact and recency layer. The linked Railway instance should be used when current context matters, but it should not overwrite the core voice guide by itself.

Use live Prism Memory for:

- current RaidGuild activity and project state
- recent Portal, Discord, GitHub, governance, and workflow signals
- examples of current agent phrasing that may reveal drift
- checking whether a public claim has source support

Before promoting anything from live Prism Memory into a durable voice reference:

1. Confirm the memory item is public-safe or sanitize it.
2. Trace it to a source digest, artifact, Portal record, repo, or approved note.
3. Decide whether it is a stable voice pattern or just recent operational phrasing.
4. Add it as a summarized pattern, not a raw dump.
5. Record the retrieval date and source class.

## Voice Model

Use a layered model:

```text
RaidGuild Core Voice
├── Institutional voice: docs, handbook, public site, brand system
├── Community voice: origin stories, member language, lived culture
├── Spice layer: punk, metal, Moloch, zine, coordination failure, DIY
├── Agent overlays
│   └── Queen Raida: useful operator + operational-occult texture
└── Channel modulation
    ├── short social
    ├── Discord/community updates
    ├── long-form editorial
    ├── website/landing pages
    ├── newsletters/email
    ├── sales/collateral
    └── scripts/media
```

The future `rg-brand-voice` skill should own this map. The future `rg-content-strategy` skill should decide which layers are appropriate for a given audience and channel.

## Extraction Workflow

### Phase 1: Corpus Inventory

Create a source ledger with:

- source name
- URL or local path
- source type
- public/private status
- voice role
- freshness
- notes about what not to extract
- retrieval method, such as GitHub repo, public article, local repo, or live Railway Prism Memory

### Phase 2: Sample Selection

Do not ingest everything equally.

Select:

- 10-20 origin stories or representative member pieces
- 5-10 institutional docs/pages
- 20-50 recent/high-signal `@RaidGuild` public posts when X access is available
- all core Queen Raida docs
- 10-20 live Prism Memory outputs that are source-grounded and public-safe
- 3-5 high-spice cultural artifacts for edge texture

### Phase 3: Audit

For each source group, extract:

- recurring nouns and verbs
- metaphors
- sentence length and rhythm
- stance toward builders, clients, agents, governance, and coordination
- common claims and caveats
- words that should be preserved
- words that should be banned or rationed
- lines that are useful as examples without being copied

### Phase 4: Synthesize

Produce references for `rg-brand-voice`:

```text
skills/rg-brand-voice/references/
├── raidguild-core-voice.md
├── community-voice.md
├── cultural-spice.md
├── queen-raida-voice.md
├── ai-solutions-voice.md
├── channel-voice.md
└── language-anti-patterns.md
```

First extraction pass completed:

- `raidguild-core-voice.md`: enriched from handbook-v2, RG brand notes, origin-story synthesis, and reviewed Prism Memory patterns.
- `community-voice.md`: added from origin stories and member-facing Prism Memory patterns.
- `cultural-spice.md`: added from origin stories, Travis Wyche high-spice cultural material, Moloch/commons framing, and Queen Raida media inspiration.
- `queen-raida-voice.md`: enriched from Queen-Raida repo docs and examples.
- `channel-voice.md`: expanded with Discord/community, buyer, and field-notes modulation.
- `language-anti-patterns.md`: expanded with RaidGuild-specific failure modes and replacement moves.

### Phase 5: Score

Every public draft can be scored on five sliders:

| Dimension | Low | High |
| --- | --- | --- |
| Formality | tavern / Discord-native | institutional / client-safe |
| Weirdness | plain operator | mythic / occult / zine |
| Specificity | broad pattern | source-heavy / named receipts |
| Authority | tentative draft | confident statement |
| Persona | RaidGuild generic | Queen Raida / named agent |

The score should be chosen before writing, not after.

## Practical Defaults

### Public RaidGuild Voice

- concrete before mythic
- builder-native
- allergic to empty SaaS claims
- specific about work, people, artifacts, and receipts
- weird only when it clarifies or gives the copy a real pulse

### AI Solutions Voice

- more client-safe
- less lore
- clear offer language
- proof discipline
- no overclaimed autonomy

### Queen Raida Voice

- practical, sharp, lightly strange
- source-grounded
- public-safe by default
- operational-occult texture only after the useful point lands
- never speaks as `@RaidGuild` HQ

### Internal/Discord Voice

- direct
- less polished
- more context-tolerant
- can preserve rough operational language
- still no secrets or private client details in public/community channels

## Refactor Impact

This does not change the target skill list. It changes how `rg-brand-voice` should be built.

`rg-brand-voice` should not be a single style guide. It should be a voice router with references for:

- core RaidGuild voice
- community/member voice
- institutional brand voice
- cultural spice
- agent persona overlays
- channel modulation
- anti-patterns

`rg-content-strategy` should decide which voice layer to apply based on audience, channel, and task.

`rg-public-output-safety` should enforce boundaries when the chosen voice gets too spicy, too private, too official, or too agent-internal.

## Live Memory Boundary

The future `rg-brand-voice` skill should know that live Prism Memory exists, but it should not directly depend on a Railway connection for every voice task.

Recommended split:

- `rg-brand-voice`: stable voice references and audit rules.
- `rg-research` or a future memory adapter reference: live Prism Memory lookup patterns.
- `rg-content-strategy`: decides when recent memory is needed for a draft.
- `rg-public-output-safety`: blocks private memory leakage and unsupported claims.

This keeps the skill portable while still letting agents use the Railway-linked Prism Memory instance when freshness matters.
