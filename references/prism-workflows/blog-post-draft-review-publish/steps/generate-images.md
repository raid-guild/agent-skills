# Generate Images

## Outcome

Generate the planned images for the approved blog draft and make the results durable for reviewer inspection.

This step should normally complete in one pass. Do not repeat a previously reported blocker unless you have new evidence that the runtime path is still impossible.

## Inputs

Use the latest available request artifacts, especially:

- the approved blog draft artifact
- `image-plan.json`
- `image-prompts.md`
- any reviewer or admin comments added after earlier generate-images attempts

If a prior attempt already produced some image artifacts or workspace files, reuse them when valid instead of regenerating everything.

## Tooling Requirement

Use Codex builtin `imagegen` for image generation when image creation is required.

- Do not treat missing OpenAI API keys, CLI image helpers, or external image services as blockers.
- Do not stop just because an API-key-based fallback is unavailable.
- The expected path for this workflow is the builtin Codex image generation capability.

## Output Contract

Target outputs:

- exactly 1 hero image
- up to 2 inline images when the media plan calls for them

Preferred durability path:

1. create request artifacts with `kind: image` for every generated image
2. create a manifest artifact that records the generated image artifact ids, intended role, and placement hints

Fallback path:

- if direct request image artifact creation is unavailable, save the generated files in the request workspace and create a manifest artifact that records:
  - workspace file paths
  - intended role (`hero` or `inline`)
  - source prompt / plan key
  - placement hints for inline images
  - any notes relevant for reviewer inspection

Manifest-only durability should be reported as fallback behavior, not as the preferred success state.

Only report the step as blocked if neither of these durability paths is possible.

## Execution Rules

- Read the image plan first and follow its requested visual roles.
- Prefer the prompts from `image-prompts.md` unless a later reviewer/admin note explicitly overrides them.
- Before declaring failure, inspect existing comments and prior run summaries so you do not repeat the same blocker message.
- If earlier runs were blocked on artifact persistence, try direct request image artifacts first, then workspace-save-plus-manifest fallback before stopping.
- If one image succeeds and another fails, keep the successful outputs and state exactly what remains missing.
- If the media plan marks inline images as optional, do not fail the step solely because one optional image was skipped.

## Reviewer Handoff

When complete, leave a concise summary that lists:

- generated image artifact ids, or workspace file paths if fallback was used
- which asset is the hero image
- which inline images were produced
- any reviewer checks, such as crop quality, label cleanup, or illustration complexity

## Output

Return a concise completion summary and move the request toward review once the images are durable enough for inspection.
