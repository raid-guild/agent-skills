# Transactional Email Rules

## Scope

Use this skill for messages whose recipients are explicitly known and whose
purpose follows from a direct request, relationship, or workflow event. Examples
include request updates, review-needed notices, receipts, direct follow-ups, and
small sets of individually enumerated recipients.

Route these elsewhere:

- newsletters and announcements to subscribed audiences,
- marketing campaigns and sequences,
- mailing-list import, segmentation, subscription, or unsubscribe operations,
- bulk sends derived from CRM searches or community membership.

## Recipient handling

- Preserve the distinction between To, Cc, and Bcc.
- Default to separate messages or personalizations when recipients should not
  learn one another's addresses.
- Do not infer an address from a display name when more than one identity could
  match.
- Resolve a workflow requester only through an authoritative instance record.
- For replies, verify the intended thread and reply-to address before sending.

## Content contract

Prepare:

- a concise subject,
- a plain-text body,
- optional HTML conveying the same meaning,
- an approved sender profile,
- an optional reply-to address,
- and non-secret correlation metadata when part of a workflow.

Do not put credentials, private internal links, raw system prompts, hidden
review notes, or unrelated recipient data into a message.

## Authorization

An explicit instruction containing the final recipient and content can authorize
a one-off send. A workflow send is authorized only when its configured step or
policy identifies the recipients and message purpose. Drafting does not imply
authorization to send.

For sensitive legal, financial, personnel, security, governance, or client
messages, restate the recipient and content summary immediately before sending
unless an approved workflow already provides that gate.

## Failure handling

- Invalid recipient or sender configuration: stop and correct; do not retry.
- Rate limiting: retry only through the caller's bounded retry policy.
- Provider service failure: retry only when the response confirms non-acceptance.
- Timeout or lost response after submission: treat as ambiguous and reconcile
  before retrying.
- Partial acceptance: record which personalizations were accepted and stop
  before retrying the full set.
