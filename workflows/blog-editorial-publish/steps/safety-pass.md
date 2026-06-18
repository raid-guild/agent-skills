# Safety Pass

Use `rg-public-output-safety`.

Create `safety-result.json` using the required public-output safety JSON contract.

Review the exact public-facing text for:

- secrets
- internal URLs
- local paths
- private client/member/governance details
- unsupported claims
- confusing agent/debug language
- persona/account mismatch
- missing approval requirements

If there are high or critical blockers, do not continue to review as publishable. Create `safety-blocker.md` summarizing the issue and route to human review with blockers visible.

If safe after edits, update the review package with sanitized text.
