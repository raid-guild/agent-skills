# Sanitize Public Output

Run a public safety pass before anything can be posted. This workflow is autonomous, so sanitizer blockers are the publish control.

Use public-social-output-sanitizer rules on:
- X post text from `x-draft.md`
- generated media prompt/alt text
- any link or launch claim

Create `sanitized-output.json` with:
- sanitized post text
- sanitizer changes
- blockers
- final media selection
- final alt text
- exact character count for the sanitized post text
- explicit publish decision: `publishable` or `blocked`

If the sanitized post text is over 280 characters, trim it to 280 characters or fewer before marking it publishable. If it cannot be trimmed without losing the required meaning, mark the output `blocked`. If there are high or critical blockers, mark the output `blocked`, do not advance into publishing, and return the blocker summary clearly. Medium/low issues may be fixed in the sanitized text before continuing.

Return a concise sanitizer summary and whether autonomous publishing may proceed.
