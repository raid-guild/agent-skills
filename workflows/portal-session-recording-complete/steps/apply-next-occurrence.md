# Apply Next Occurrence

Use `rg-portal-ops`.

This agent node has `autoRun: false`. Continue only when the operator accepts the recurrence plan or the event source is trusted for automatic recurrence.

Apply the exact `next-occurrence-plan.md` to Portal. Do not invent missing time, title, location, guests, or join context.

Re-read Portal after writing and produce `next-occurrence-verification.json` with created/updated record id, URL, copied fields, omitted fields, and failures.
