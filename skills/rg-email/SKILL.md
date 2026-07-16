---
name: rg-email
description: Use when Codex needs to draft, preview, send, or reconcile an approved RaidGuild transactional or one-off email using the instance's configured email provider credentials, including explicit-recipient messages, small individually enumerated recipient sets, workflow notifications, replies, and delivery evidence. Not for newsletters, marketing campaigns, mailing-list management, or audience expansion.
---

# RaidGuild Email

Use this skill for private transactional email operations after the purpose,
recipients, and authority to send are clear.

This skill owns email preparation, approval checks, provider invocation, and
delivery evidence. It does not own campaign strategy, bulk lists, subscription
state, credential custody, or workflow-event polling.

## Routing

Read only the references needed:

- Message, recipient, approval, and privacy rules:
  `references/transactional-email.md`
- SendGrid configuration, request shape, and response handling:
  `references/sendgrid.md`

Use `rg-brand-voice` when the message needs RaidGuild voice work.
Use `rg-public-output-safety` when email content will also be published.
Use the instance campaign system for newsletters, mailing lists, or bulk sends.

## Modes

- `DRAFT`: prepare subject, recipients, text/HTML body, and send plan.
- `PREVIEW`: validate the exact outbound envelope without sending.
- `SEND`: perform an authorized email send through the configured provider.
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

## Credential Boundary

Use conventional environment variables supplied to the trusted job by the
instance credential system. For SendGrid, follow `references/sendgrid.md`.
Never ask the operator to paste a key into chat or task input.

Check only whether required variables are present. Never print, persist, return,
or interpolate secret values into commands, logs, artifacts, or error messages.
If configuration is missing, report the missing variable names and direct the
operator to add or update the email credential in instance Settings.

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
