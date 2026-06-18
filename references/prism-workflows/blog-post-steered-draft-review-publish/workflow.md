# Blog Post Steered Draft Review Publish

This workflow creates one-off topic-specific blog posts only after a human provides steering in the request comments and approves the intake gate.

The request must not auto-run into drafting from submission alone. Intake is a human gate: if no steering comment exists, the workflow stays at intake and waits for human direction.

After intake approval, Codex drafts the post, prepares a media plan, generates image assets when requested, waits for human review, revises if needed, prepares a Payload CMS draft, and publishes only when the workflow reaches the publish step.

Durable outputs should be stored as request artifacts. Live CMS records or external publishing targets should be attached as external refs when created.
