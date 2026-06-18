# Publish Queen Raida Article

This workflow creates one public Queen Raida website article in the repository https://github.com/raid-guild/Queen-Raida.

The workflow is intentionally narrow. It is only for article changes under the Queen Raida site, and the expected target app is the registered Queen Raida target source with repo URL https://github.com/raid-guild/Queen-Raida and default branch main.

The authoritative implementation guide is site/AGENTS.md in the target repository. Agents must follow that file before making article changes, especially the article location, frontmatter, slug, tone, validation, and privacy rules.

## Flow

1. Triage confirms the article request is suitable, scoped to the Queen Raida site, and supported by enough public source material.
2. Approve is a human gate before repository work begins.
3. Work creates the article markdown artifact, implements the article change in the target repo, validates it, opens or updates a PR, and attaches the PR as an external ref.
4. Review is the human acceptance gate for the article artifact and PR. Approved closes the workflow. Changes requested returns to Work.

## Durable State

Request state, approvals, executions, events, artifacts, and external refs belong in Prism DB-backed records. Do not store workflow progress in markdown files.

The key artifact is the article markdown. It should be saved through the request artifact API as a markdown artifact before or alongside the repo change so reviewers can inspect the article content without opening the branch.

## Safety

Only publish public, supportable claims. Do not include secrets, private Discord content, private client details, private member information, internal operational notes, unsupported governance claims, or source links that should not be public.

If public evidence is insufficient, triage or work should stop with a clear request for missing source material instead of inventing details.
