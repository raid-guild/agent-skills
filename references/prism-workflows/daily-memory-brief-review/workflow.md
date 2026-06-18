# Daily Memory Brief Review

This workflow creates a concise Prism Memory brief for the current day or weekday context, pauses for human review, publishes the approved brief into Payload CMS as a draft, and closes when the workflow is complete.

## Purpose

Use this workflow when a scheduled process should open a reviewable content request instead of directly posting a memory brief to an output channel.

## Human Gate Behavior

The review step is the required human gate.

- approved -> publish
- changesRequested -> revise
- rejected -> closed

## Durable State

Brief drafts, source notes, and publish receipts should be stored as request artifacts or execution outputs, not in workflow markdown.
