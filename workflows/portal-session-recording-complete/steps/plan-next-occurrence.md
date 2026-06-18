# Plan Next Occurrence

Use `rg-portal-ops`.

Inspect the session recurrence metadata and produce `next-occurrence-plan.md`.

Include:

- whether the session is recurring
- current recurrence rule or inferred pattern from explicit Portal data
- proposed next occurrence date/time
- fields to copy
- fields to reset or omit
- reason to skip recurrence if not applicable

Route:

- `apply` -> `apply-next-occurrence` when a concrete next occurrence can be created or updated
- `skip` -> `closed` when recurrence does not apply or is ambiguous
