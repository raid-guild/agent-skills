Prepare and validate the FiresideRecapScene render envelope.

Use remotion-composition-checker behavior or direct HTTP checks against https://remotion-service-production.up.railway.app:
- GET /compositions
- GET /compositions/FiresideRecapScene/schema
- GET /schemas

Read recap-plan.json, youtube-description.md, and tts-manifest.json. Upload all MP3 segment artifacts to the configured workflow audio bucket using workflow-audio-bucket-uploader patterns. Verify every uploaded audio URL is publicly fetchable without service-token auth before inclusion.

Build remotion-input.json with exactly this shape:
{
  "composition": "FiresideRecapScene",
  "outputKey": "firesides/<safe-session-slug>-recap.mp4",
  "props": {
    "title": "...",
    "subtitle": "...",
    "introAudioUrl": "...",
    "introDurationMs": 0,
    "guest": {"name":"...","handle":"...","avatarUrl":"..."},
    "host": {"name":"...","handle":"...","avatarUrl":"..."},
    "backgroundUrl": "...",
    "cards": [{"title":"...","body":"...","quote":"optional","imageUrl":"...","audioUrl":"...","durationMs":0}],
    "outro": {"headline":"Watch the full interview","url":"portal.raidguild.org","audioUrl":"...","durationMs":0}
  }
}

Required schema fields to enforce before render:
- props.guest.name
- props.guest.handle
- props.guest.avatarUrl
- props.cards[0].title
- props.cards[0].body

Also enforce exactly 5 cards unless a human explicitly approved another count. Set each durationMs to measured audio duration plus 700-1200ms.

Create remotion-input.json and render-plan.json. If schema discovery fails or required fields/assets are missing, create remotion-prep-blocker.md and stop.
