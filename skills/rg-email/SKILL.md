---
name: rg-email
description: Use when Codex needs to draft, preview, send, or reconcile an approved RaidGuild transactional or one-off email through an assigned email Gateway toolset, including explicit-recipient messages, small individually enumerated recipient sets, workflow notifications, replies, and delivery evidence. Not for newsletters, marketing campaigns, mailing-list management, audience expansion, or sending without explicit recipient and content authorization.
---

# RaidGuild Email

Use this skill for private transactional email operations after the purpose,
recipients, and authority to send are clear.

This skill owns email preparation, approval checks, safe Gateway invocation, and
delivery evidence. It does not own campaign strategy, bulk lists, subscription
state, provider credentials, or workflow-event polling.

## Routing

Read only the references needed:

- Message, recipient, approval, and privacy rules:
  `references/transactional-email.md`
- Gateway invocation and SendGrid-specific behavior:
  `references/sendgrid-gateway.md`

Use `rg-brand-voice` when the message needs RaidGuild voice work.
Use `rg-public-output-safety` when email content will also be published.
Use the instance campaign system for newsletters, mailing lists, or bulk sends.

## Modes

- `DRAFT`: prepare subject, recipients, text/HTML body, and send plan.
- `PREVIEW`: validate the exact outbound envelope without sending.
- `SEND`: perform an authorized email send through the assigned Gateway toolset.
- `RECONCILE`: inspect safe response evidence and report accepted, rejected,
  ambiguous, or failed status.

## Send Gate

Before `SEND`, confirm:

1. The exact To, Cc, and Bcc recipients are explicit.
2. The subject and final body are known or reference an approved template.
3. The sender identity and reply-to policy are configured.
4. The current user request or workflow authorizes the external send.
5. The operation is transactional or one-off, not a campaign/list send.

If any item is missing, remain in `DRAFT` or `PREVIEW`.

## Gateway Boundary

Use the assigned email Gateway toolset. Call its canonical `describe` operation
before the first use in a session, then use `request` according to the returned
schema. Do not call a provider using a pasted key or ask the operator to reveal
one.

If the toolset is unavailable, report the missing email integration and direct
the operator to configure or assign it through Gateway. Do not fall back to
credentials in chat, skill files, task params, artifacts, or command history.

## Operating Rules

- Treat recipient addresses and message bodies as private data.
- Do not expose recipients to each other accidentally; use separate
  personalizations or Bcc when appropriate.
- Do not add recipients inferred from CRM, chat, or a mailing list unless the
  authorized operation explicitly selects them.
- Keep workflow correlation ids non-secret and exclude private content from
  provider metadata.
- Treat provider acceptance as accepted-for-delivery, not proof of delivery.
- Do not automatically retry an ambiguous send; avoid duplicate email and
  report the uncertainty.
- Capture only safe evidence such as provider message id, accepted timestamp,
  recipient count, template key, and correlation id.

## Output

For drafts and previews:

```text
Email plan:
- mode:
- purpose:
- to/cc/bcc:
- subject:
- sender profile:
- reply-to:
- template or body summary:
- approval status:
- privacy concerns:
- blockers:
```

For sends and reconciliation, report the safe plan fields plus the result,
provider message id when available, correlation id, and any retry guidance.
