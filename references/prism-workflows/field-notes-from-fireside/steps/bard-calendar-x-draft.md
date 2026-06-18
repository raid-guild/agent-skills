Create exactly one X post draft in Bard Calendar for later human review and scheduling. Use bard-calendar-ops as the authoritative interface.

Source basis:
- Use the approved source pack, topic/angle map, media brief, and Portal event artifact/resource links.
- The draft should promote the session/event and point to the strongest source-grounded takeaway without overclaiming.
- Fireside recap drafts must target channel `x: main account`. Do not use `discord`, `x`, `x: raida`, or any other target channel unless the request explicitly overrides the account.

Safety and review boundary:
- Run public-social-output-sanitizer before storing the draft.
- Do not publish to X.
- Do not create more than one X draft from this parent workflow unless the request explicitly asks for variants.
- Scheduling is allowed only as a planned Bard Calendar event. It is not publishing.

Bard Calendar scheduling rules:
1. Before creating or assigning any publishing event, query upcoming Bard Calendar events for at least the next 7 days, including planned, scheduled, ready, draft, and published statuses when available.
2. Look for an existing planned event that can fit the same fireside recap. A fitting event has compatible campaign/source context, target channel `x: main account`, and notes/title indicating the same session, same combined fireside recap, or a flexible fireside recap slot.
3. If a fitting event already exists, attach or assign the draft to that event instead of creating a new event. Preserve its date/time unless there is a clear conflict.
4. If no fitting event exists, choose a publish time by inspecting the existing schedule. Avoid adding more than one main-account fireside recap on the same day unless the user explicitly asks for that cadence.
5. Prefer a day with no existing `x: main account` fireside recap. If there is already a related recap planned that day, either reuse it for a combined recap or choose another day.
6. Keep at least one reasonable spacing window from other major `x: main account` posts where possible. Default candidates are 16:00 UTC or 18:00 UTC on the next open weekday, but the schedule query should drive the choice.
7. Record the scheduling rationale in the Bard event notes and in the request artifact. Include which existing events were considered, whether one was reused, and why the selected slot was chosen.

Bard Calendar record guidance:
- Channel/platform: `x: main account`.
- Draft status: `draft` unless the copy has already been approved.
- Publishing event status: `planned` if a publish slot is assigned.
- Campaign/source metadata should reference field-notes-from-fireside, the parent request number/id, Portal event id, and source artifact URLs.
- Include the sanitized draft text, source links, candidate topic/title, any caveats, and the schedule rationale.
- Do not create a new event with target_channel `discord` for a fireside recap.

Output:
- Create or update a request artifact named bard-calendar-x-draft-result.json with the Bard Calendar topic id, draft id, event id if assigned, status, planned channel, planned publish time if any, whether an existing event was reused, schedule rationale, draft text, source refs, and sanitizer changes/blockers if any.
- Return a compact summary with the calendar item id/status, channel, scheduling decision, and confirm no X publishing occurred.
