# Lore Entry Draft Review Publish

This workflow creates serialized fictional lore entries for the RaidGuild / Queen Raida world. It should feel like an evolving short-story arc, not a newsletter, recap, product update, or generic blog post.

## Purpose

Use this workflow when an operator wants a public lore post that turns real RaidGuild, Queen Raida, proposal, memory, project, or cultural context into a fictionalized world fragment. The entry should be grounded in known context while avoiding unsupported claims about real people, private details, or operational secrets.

The workflow produces:
- a durable intake brief
- a continuity / arc plan
- a complete lore entry draft
- image direction and generated image artifacts
- a human review gate
- a Payload CMS draft with tags including `lore`

## Editorial Direction

The entry should read like a short story fragment from an expanding world: scene, tension, image, object, omen, signal, character motion, and consequence. It should not read like a newsletter, community update, meeting digest, or announcement.

Queen Raida and RaidGuild context are inspiration and source material. The story may use guild-coded motifs such as raids, taverns, keepers, signal fires, proposal halls, agents, coordination rituals, memory engines, portals, vaults, spoils, quests, and builders, but it must remain public-safe and clearly fictionalized.

## Required Knowledge Grounding

Agents should use Prism Knowledge and Memory when useful, especially:
- Queen Raida persona and media inspiration docs
- RaidGuild handbook / portal / project knowledge
- recent public-safe memory or proposal context when relevant to the requested theme

Do not invent factual claims about RaidGuild operations. When using real context, transform it into fictional motif and keep any factual source notes internal to artifacts for reviewer verification.

## Human Gate Behavior

The review step is required.

- approved -> publish-prep
- changesRequested -> revise
- rejected -> closed

Review should check story quality, continuity, public safety, image fit, and whether the piece avoids newsletter voice.

## Durable State

Save all important outputs as request artifacts:
- `lore-intake.md`
- `lore-arc.md`
- `draft.md`
- `media-plan.md`
- generated image artifacts or image manifest
- `publish-package.json` or `publish-package.md`
- `publish-receipt.md`

Later steps should read these artifacts rather than relying on chat history.

## Publishing Contract

Publish to Payload CMS as a draft unless explicitly instructed otherwise. The CMS post must include the tag `lore`. If category fields exist, prefer a lore/story/worldbuilding category when available, but do not block on category creation unless the CMS requires it.

Generated images selected for the post should be embedded in the post body or clearly attached as featured / inline media according to CMS capabilities. Uploading media without placing or selecting it should be called out as incomplete.
