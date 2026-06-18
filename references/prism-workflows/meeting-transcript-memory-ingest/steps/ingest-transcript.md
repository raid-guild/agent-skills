Use change-request-ops to inspect the current request, comments, artifacts, and attached files through /agent/* routes. Find the transcript file attached during the human gate. Do not proceed if no transcript file is attached; instead return a clear needs-human-input result saying the transcript file is missing.

Read the attached transcript content. Preserve the transcript text as the memory inbox content. If the attachment is JSON, extract the most transcript-like textual field or serialize the transcript messages in readable order; do not invent missing speaker labels.

Write one Prism Memory inbox item using prism-api-writer and POST /memory/inbox with:
- source: "manual-meeting-transcript-upload"
- bucket: comment-provided bucket if present, otherwise "meetings"
- type: "meeting_transcript"
- ts: meeting date/time from request/comment/file metadata if present, otherwise current UTC timestamp
- content: transcript text plus a short source header containing request number/id and original filename
- author: "meeting-transcript-ingest-agent"
- participants: parsed or comment-provided participants when confidently available
- participant_count: count of participants when confidently available
- metadata: include source_system "manual-upload", source_type "meeting_transcript_file", original_filename, request_id, request_number, workflow_key, meeting_title if provided, meeting_date if provided, transcript_format if known, and external_refs/artifact refs for the attachment when available.

After the inbox write, create or attach a concise request artifact named "meeting-transcript-memory-ingest-result.json" containing the memory inbox response, source filename, selected bucket, selected ts, participant list if any, and any caveats. Do not call /ops/* and do not run memory backfills or pipeline ops. Return a compact completion summary with the inbox item id or artifact id returned by the API.
