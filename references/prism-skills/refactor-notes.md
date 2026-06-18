# Prism Refactor Notes

## Initial Hypothesis

The current Prism skill set mixes reusable capabilities, tool operations, personas, aliases, and one-off workflows. The refactor should reduce the number of published skills by assigning each durable concept to one owner.

## Likely Shared Owners

### Public Output Safety

Absorbs repeated checks for:

- Secrets and credentials
- Client-private information
- Internal URLs and local paths
- Unsupported claims
- Debug or agent-process language
- Public account/persona mismatch

### Brand and Voice

Owns RaidGuild voice, AI Solutions voice, Queen Raida voice, tone modulation, anti-patterns, and channel-specific voice rules.

### Content Strategy

Owns campaign planning, editorial framing, content pillars, audience mapping, idea generation, draft evaluation, and repurposing.

### Research

Owns source quality, current-event checks, community/news scanning, claim verification, and citation discipline.

### Publishing Operations

Owns mechanics and approval gates for public channels such as X, Discord, Portal CMS, calendars, queues, and live URLs.

## Open Questions

- Which Prism skills are still actively used?
- Which skills have actual scripts or tools versus only instructions?
- Which operations can be dry-run or read-only?
- Which skills contain private client or credential-adjacent material that must stay out of this repo?
- Should this repo publish cross-client skills only, or Codex-specific metadata too?
