# Brief Media Publish

This workflow creates source-backed RaidGuild briefs, public summaries, internal summaries, podcast scripts, audio/video media, and Portal publish drafts.

Use it for:

- weekly public brief with podcast/video
- internal daily member brief with podcast/video
- daily memory brief without media
- fireside recap video from a completed Portal session
- brief-only public or internal summary when no media should be rendered

## Canonical Shape

1. Human steering gate confirms source mode, time window, visibility, and media requirement.
2. Source intake builds a source ledger and evidence brief.
3. Brief plan selects audience, visibility, format, and story spine.
4. Draft brief creates the written summary.
5. Script plan either prepares podcast/video script artifacts or marks the run as brief-only.
6. Human content review approves written copy and script before generation.
7. TTS, storage, Remotion prep, render, and checkpoint run only for media modes.
8. Final review approves rendered media.
9. Publish prep validates links, public safety, and Portal payload shape.
10. Publish runs with operator continuation and records evidence.

## Source Modes

- `weekly_public`: public weekly RaidGuild brief, public-safe and CTA-oriented.
- `internal_daily`: member/internal brief that may include private operational context.
- `daily_memory`: concise Prism Memory brief, usually brief-only.
- `fireside_recap`: one completed Portal fireside session with recap video.
- `brief_only`: written brief without TTS or video render.

## Skill Composition

- `rg-content-strategy`: source ledger, brief angle, audience, format, and story spine.
- `rg-brand-voice`: public RaidGuild voice, member/internal tone, and host script tone.
- `rg-public-output-safety`: public copy, descriptions, titles, and social summaries.
- `s3-object-storage`: upload generated audio or render input assets.
- `rg-media-render-ops`: Remotion composition inspection, payload prep, render submission, and status checks.
- `rg-portal-ops`: Portal draft, brief, post, wiki, session resource, or CMS update.
- `rg-publishing-ops`: Discord summary, calendar/X draft, or external publish evidence.

## Operator Semantics

The first node is a human gate, so open-ended brief runs wait for steering before agent work begins. Media generation can continue automatically after content approval, but the final publish node has `autoRun: false` so an operator explicitly continues the live write/update step.
