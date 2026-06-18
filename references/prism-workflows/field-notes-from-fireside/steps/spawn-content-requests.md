# Spawn Content Requests

Create follow-on content production requests from the approved Field Notes From Fireside package.

This step runs after angle review and Bard Calendar X draft creation. It should not draft, publish, render, or schedule the child content itself. Its job is to create traceable child requests that a human can review and start later.

## Inputs

Read the parent request, comments, external refs, and artifacts from this workflow, especially:

- source pack / source ledger
- angle plan or topic map
- media brief
- Portal session/event artifact resource details
- Bard Calendar X draft result
- any human review comments from Angle Review

If required upstream artifacts are missing, create a blocker artifact named `spawn-content-requests-blocker.md` and stop with a concise blocker summary. Do not create partial or duplicate child requests when the parent package cannot be identified.

## Reconcile Before Creating

Before creating anything, inspect existing external refs, request links, comments, and child-request evidence for this parent request. Reuse or report existing children instead of creating duplicates.

A child request counts as existing when it is clearly tied to this parent fireside session and workflow key, even if its title changed.

## Required Child Requests

Create one non-autostart child request for each follow-on workflow:

1. `fireside-blog-post-draft-publish` - a focused blog post from the strongest approved fireside angle.
2. `fireside-wiki-topic-develop` - one or more Portal wiki topic pages from the approved topic map.
3. `fireside-recap-video-publish` - a source-grounded recap video for the completed Portal fireside session.

Use `POST /agent/change-board/requests` with `x-service-token` auth. Set `autoStart: false` for every child so it is queued for later human review/start, not immediately run from this parent workflow.

Use `requestType: "content"`, `priority: "normal"` unless the parent request explicitly says otherwise, and include a coarse `estimatedHumanHours` bucket when the scope is clear.

Each child request description must include:

- the parent request number/id
- the Portal session/event URL or id when available
- the approved angle/topic it should handle
- links or ids for the source pack, angle plan/topic map, media brief, Bard Calendar draft, and Portal artifact resources
- clear instruction that the child must ground all claims in the parent artifacts and session sources
- any missing inputs or human notes from the parent gate

For the recap video child, include the completed Portal session/event URL or id, transcript/summary/source artifact links, guest/host fields if known, and the media brief. State that the child workflow should render through `fireside-recap-video-publish` and attach final video artifacts back to the Portal session when approved.

## Traceability

After creating or finding the children:

- attach external refs to the parent for each child request using provider `prism`, kind `child_request`, and metadata containing the child workflow key and purpose
- create `spawned-content-requests.json` with the parent request id/number and one entry per child: workflowKey, title, request id/number, URL if available, autoStart, purpose, and reused vs created
- add a concise parent comment or final step summary listing the child request numbers and confirming that all were created with `autoStart: false`

Do not mark this step complete unless all three child workflows are represented or a blocker artifact explains why not.
