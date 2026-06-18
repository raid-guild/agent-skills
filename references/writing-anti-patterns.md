# RaidGuild Writing Anti-Patterns

Use this as source material for future `rg-brand-voice`, `rg-content-strategy`, and `rg-public-output-safety` references. It is not a published skill.

The goal is not to make copy bland. The goal is to prevent RaidGuild output from collapsing into generic AI, corporate SaaS, or fake-mystic sludge.

Refresh this periodically. Model defaults change.

## Lexical Tells

Words and phrases to challenge when they appear in public copy.

| Pattern | Why It Fails | Better Move |
| --- | --- | --- |
| leverage | corporate filler | use a concrete verb |
| synergy / synergize | empty business language | say what combines and why |
| robust | vague unless literal | name the property: tested, durable, fault-tolerant, simple |
| seamless / seamlessly | overclaimed UX language | describe the actual handoff or integration |
| unlock | value-prop filler | say what becomes possible |
| empower | vague uplift | say who can do what |
| supercharge | hype | give the concrete acceleration or improvement |
| cutting-edge | unsupported status claim | name the new method, tool, or constraint |
| revolutionary / game-changing | inflated claim | use evidence or remove |
| next-gen / next-generation | generic tech marketing | name the generation shift |
| delve / dive into | AI-default opener | start with the subject |
| crucial / pivotal | false urgency | explain the consequence |
| dynamic / vibrant | placeholder adjective | give a visible signal |
| holistic | hand-wavy | list the actual components |
| paradigm | usually inflated | say model, pattern, or approach if needed |
| foster | NGO/corporate mush | build, support, fund, host, coordinate |
| utilize | stiff | use |
| facilitate | often vague | help, let, host, coordinate |
| ecosystem | overused | name the people, tools, protocols, or market |
| journey | generic narrative filler | name the stage, process, or decision |
| passionate / mission-driven | self-flattery | show the work or motivation |

## Phrase Tells

Rewrite these rather than swapping one word.

- "In today's fast-paced world..."
- "In the ever-evolving landscape..."
- "It's not just X, it's Y."
- "It's important to note..."
- "It's worth noting..."
- "Let's dive in."
- "Let's unpack."
- "Picture this."
- "Imagine a world where..."
- "What if I told you..."
- "Whether you're a seasoned expert or just getting started..."
- "At the end of the day..."
- "Last but not least..."
- "Hope this helps."
- "Click here to learn more."
- "We are excited to announce..." unless excitement is genuinely the point.

## RaidGuild-Specific Anti-Patterns

### Fake Guild Voice

Avoid lore texture that hides the point.

Weak:

- "The guild has opened a powerful new ritual orchestration layer."
- "The machine spirits have blessed our community activation surface."

Better:

- Say what shipped, who can use it, and where the weirdness belongs.
- Use lore as seasoning after the factual payload lands.

### Agent Process Leakage

Public copy should not expose workflow machinery unless the audience needs it.

Cut or rewrite:

- "Prism Memory says..."
- "The workflow step generated..."
- "Artifact id..."
- "I used the Portal API..."
- raw JSON, logs, stack traces, internal route names, task ids, local paths

### Unsupported Status Claims

Do not imply:

- a client approved something unless source material says so
- a product is launched if it is only drafted, staged, or under review
- a governance proposal passed before live evidence confirms it
- an agent acted autonomously if a human approval gate was required
- a public URL exists when only an internal artifact URL exists

### Account Confusion

Queen Raida / `@raidguildish` can reference RaidGuild but must not speak as `@RaidGuild` HQ or imply human membership, governance authority, or official client commitments.

## Structural Tells

| Pattern | Risk | Counter |
| --- | --- | --- |
| repeated three-item lists | default AI rhythm | vary list length or use prose |
| colon headlines | generic thought-leadership smell | use a direct title when possible |
| symmetric paragraphs | machine cadence | vary paragraph length |
| summative closers | unnecessary recap | end on the strongest point |
| too many bullets | outline instead of writing | use bullets only for scan value |
| unsupported hedges | weak authority | cite, qualify, or cut |
| repeated openers | visible template | change sentence structure |

## Opener Kill List

These should usually fail an editorial pass:

- "In today's fast-paced world..."
- "Have you ever wondered..."
- "Did you know..."
- "What if I told you..."
- "In this post, we'll explore..."
- "Hot take:"
- "Unpopular opinion:"
- "Recently..." without a concrete date
- "At RaidGuild, we believe..." unless the belief itself is the news
- dictionary-definition openers
- three rhetorical questions in a row

## Punctuation And Rhythm

Do not treat punctuation as proof that a draft is AI-generated. Treat it as a pattern to inspect.

Check for:

- em dash density that makes every sentence feel the same
- ellipses outside direct quotation
- stacked parenthetical asides
- long runs of same-length sentences
- repeated "X, Y, and Z" cadence

Better rhythm usually comes from concrete editing:

- cut throat-clearing
- shorten the sentence that carries the point
- vary list length
- put the factual noun earlier
- let one short sentence stand alone when it earns the break

## Audit Checklist

When auditing a draft:

1. Search for lexical tells and phrase tells.
2. Check whether every strong claim has a source or concrete evidence.
3. Check for leaked workflow, tool, API, artifact, or internal path language.
4. Check whether lore or brand flourish obscures the factual point.
5. Check for repeated three-part rhythm, generic openers, and summative closers.
6. Rewrite the thought, not just the flagged word.
7. If the draft is public, route it through the future `rg-public-output-safety` skill before posting, queueing, or sending for approval.
