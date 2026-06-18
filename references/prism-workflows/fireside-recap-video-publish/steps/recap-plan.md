Create the content plan for a FiresideRecapScene video from the completed session sources.

Read session-source-pack.json plus transcript, summary, and attached artifacts.

Required outputs:
- Exactly 5 key highlights for recap cards. Each card needs title, body, optional source quote, source evidence URL/id, and visual direction.
- A concise title and subtitle for the video.
- Guest and host object candidates: name, handle, avatarUrl. Required fields for render are guest.name, guest.handle, guest.avatarUrl. If any are missing, create recap-plan-blocker.md instead of guessing.
- Intro narration script, one narration script per card, and outro narration script. Keep scripts punchy and spoken, usually 15-35 seconds per segment.
- A YouTube description draft with: 2-3 sentence summary, 5 highlight bullets, source/session link, Portal CTA, and credits.
- A render asset plan: backgroundUrl, card imageUrl choices, avatar URLs, and any missing assets. Prefer stable existing public URLs or Remotion /assets paths when available.

Source discipline:
- Pull highlights from attached artifacts and transcript/summary only.
- Do not fabricate quotes, claims, guest handles, product status, or attendee identity.
- Preserve uncertainty if an artifact is ambiguous.

Create recap-plan.json and youtube-description.md. Route to review.
