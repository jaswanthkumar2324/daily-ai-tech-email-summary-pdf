# Runbook

## Normal Run Flow

1. Read `memory.md` before doing any work.
2. Record the run start time in Asia/Calcutta.
3. Search Gmail with a bounded query covering the last 48 hours.
4. Sort messages by timestamp and keep only messages within the last 24 hours.
5. Use lightweight listing first. Hydrate full message content only when snippets are insufficient.
6. Extract editorial content and remove newsletter filler.
7. Merge overlapping topics.
8. Research each retained topic on the web for a small amount of extra factual context.
9. Generate a compact PDF with title/date and topic headings only.
10. Find same-name files in the target Google Drive folder.
11. Replace the existing file for the same date, or upload a new file if none exists.
12. Update `memory.md` with the outcome.

## Gmail Query Strategy

Use sender filtering and inbox scope. Example shape:

```text
(from:superhuman OR from:rundown) in:inbox after:YYYY/MM/DD
```

Then apply strict timestamp filtering locally:

```text
message timestamp >= run_start - 24 hours
message timestamp <= run_start
```

This avoids timezone edge cases while keeping Gmail queries efficient.

## PDF Format

Keep it simple:

```text
AI & Tech Summary
May 16, 2026 - Asia/Calcutta

OpenAI AI Agent Phone
- Bullet with newsletter fact plus researched context.
- Bullet with another useful fact.
- Bullet with implication or status.
Links: Source 1 | Source 2
```

Do not add category or recap sections unless the user explicitly changes the format again.

## Drive Handling

Target folder:

```text
1jNK2aGo6Cpy_iiKzaVXNLAmGJIUWSfFd
```

Use the Drive `/files` endpoint for search/verification when using proxy execution. Do not use `/drive/v3/files`; that path causes a doubled `/drive/v3/drive/v3/files` request in the connector.

## Failure Handling

- No emails: generate a PDF saying no matching emails were found.
- PDF generation failure: retry once with a simpler layout.
- Drive upload failure: retry once.
- Replacement failure: upload as `_retry1`.
- One sender missing: continue with the other senders.
