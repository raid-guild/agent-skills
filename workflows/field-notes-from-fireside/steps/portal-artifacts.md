# Portal Artifacts

Use `rg-portal-ops`.

Attach source and planning artifacts to the Portal session/event resources.

Preserve existing resources. Add stable resource labels such as:

- Source pack
- Topic map
- Media brief
- Session transcript
- Session summary
- Session recording

Do not create or update Portal posts. Do not create or update Portal wiki pages.

If generated artifacts are protected request artifacts, mirror them through the configured human-viewable artifact path before linking them from Portal resources.

Produce `portal-event-artifacts-verification.json` with event id, resource labels, URLs, resource types, mirrored artifact ids if any, and failures.
