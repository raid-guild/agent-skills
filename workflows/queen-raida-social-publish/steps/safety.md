# Safety Pass

Use `rg-public-output-safety`.

Run the sanitizer against every candidate in `queen-raida-social-drafts.md`.

Produce `queen-raida-social-safety.json` using the public output safety contract. Include:

- sanitized text for each candidate
- changes made
- blockers
- risk level
- whether the candidate is safe for human review

Route:

- `clear` -> `review` when at least one candidate has no high or critical blocker
- `needsRevision` -> `revise` when minor or medium issues can be fixed directly
- `blocked` -> `review` when high or critical blockers require operator judgment
