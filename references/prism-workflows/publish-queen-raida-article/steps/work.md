# Work

## Outcome

Create the Queen Raida article markdown, implement it in the target repository, validate the site, and open or update a pull request.

## Required Context

Use the linked change request, triage notes, existing artifacts, operator comments, and target app metadata. Work only in https://github.com/raid-guild/Queen-Raida, default branch main, under the site project.

Before editing, read site/AGENTS.md from the target repository and follow it as the authoritative guide. It defines the article format, expected frontmatter, content conventions, tone, file placement, and validation commands.

## Article Artifact

Create or update a markdown artifact containing the article body and frontmatter. Use a durable name such as article.md unless the request specifies a better artifact name.

The artifact should reflect the content intended for the repository file. If the repository implementation changes the article during editing, update the artifact so it remains reviewable.

## Implementation

Create a request branch from main unless an appropriate linked PR or branch already exists. Reconcile existing work before starting a duplicate branch or PR.

Implement only the article change needed for this request. Avoid unrelated refactors or broad site changes.

Use public, supportable claims only. Apply public output sanitization before opening the PR or returning for review.

Run validation from the site directory:

- npm run lint
- npm run build

If validation cannot run, report why and include the residual risk.

## External Refs

Open or update a pull request against the Queen Raida repository main branch. Attach the PR as a GitHub pull_request external ref on the change request. If a PR ref already exists, update or reuse it instead of creating a duplicate.

## Completion

Return a concise summary with:

- Article artifact name
- Repository file changed
- PR URL or reason no PR was opened
- Validation commands and results
- Any remaining review notes

Recommend moving to the Review gate when the article artifact and PR are ready for human review.
