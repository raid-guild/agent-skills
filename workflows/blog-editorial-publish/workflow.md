# Blog Editorial Publish

Canonical editorial/blog workflow for RaidGuild posts.

This recipe absorbs the generic, steered, fireside, and lore blog workflows while keeping mode-specific instructions explicit. It starts with a human steering gate so the operator can choose the source mode, audience, angle, constraints, and publishing expectation before agent work begins.

## Source Modes

- `generic`: normal blog/editorial post from user-provided or Prism-backed context.
- `steered`: one-off post that must wait for a steering comment before drafting.
- `fireside`: focused post from a fireside session topic, source pack, or mature wiki topic.
- `lore`: serialized fictional/lore entry grounded in Queen Raida/RaidGuild motifs and public-safe context.

## Skill Sequence

1. `rg-content-strategy`: audience, source ledger, angle, content job, format.
2. `rg-brand-voice`: RaidGuild, AI Solutions, Queen Raida, or lore voice fit.
3. `rg-public-output-safety`: final safety review before public-ready handoff.
4. `rg-portal-ops`: Portal post draft/publish package and CMS record handling.
5. `rg-publishing-ops`: only if the approved post also needs external scheduling, announcement, or live URL reconciliation outside Portal.

## Outputs

Durable artifacts should include:

- `strategy-brief.md`
- `draft.md`
- `media-plan.md`
- `voice-pass.md`
- `safety-result.json`
- `review-package.md`
- `publish-package.json`
- `publish-receipt.json` when a Portal record is created or updated

## Execution Notes

- The first node is a human gate and always waits.
- Most agent nodes use `autoRun: true` after steering.
- `portal-write` uses `autoRun: false` because a Portal write is an external CMS operation and should be operator-started unless a runtime explicitly chooses to relax that gate.
- Source exports remain under `references/prism-workflows/` for auditability.
