# Daily AI & Tech Email Summary PDF

Codex automation that runs daily at 9:00 PM Asia/Calcutta and creates a compact PDF briefing from recent AI and technology newsletters.

## What It Does

- Searches Gmail inbox messages from the last 48 hours from:
  - Superhuman
  - The Rundown Tech
  - The Rundown AI
- Sorts by message timestamp and keeps only messages from the last 24 hours from run start.
- Hydrates full email content only when lightweight previews are not enough.
- Removes ads, sponsor blocks, referral links, unsubscribe text, repeated footers, and boilerplate.
- Deduplicates overlapping stories by topic.
- Adds researched context for each retained topic using browser/web research.
- Generates `AI_Tech_Summary_YYYY-MM-DD.pdf`.
- Uploads or replaces the PDF in Google Drive folder:
  `1jNK2aGo6Cpy_iiKzaVXNLAmGJIUWSfFd`

## Current Output Style

The PDF intentionally stays simple:

- Title: `AI & Tech Summary`
- Date in Asia/Calcutta
- One heading per actual topic
- Short factual bullets under each heading
- Clickable links for useful original or reputable sources

It should not include extra sections such as:

- Most Important Updates
- Quick 30-Second Read
- Things Worth Exploring Later
- Category headings
- Sources

## Files

- `automation.toml` - Codex automation definition.
- `memory.md` - Latest automation memory and formatting decisions.
- `docs/runbook.md` - Operational notes for running and maintaining the automation.

## Requirements

This automation expects Codex Desktop with connected apps:

- Gmail
- Google Drive

The automation also needs browser/web access during runs so each topic can be lightly researched before the PDF is generated.

## Schedule

```text
FREQ=DAILY;BYHOUR=21;BYMINUTE=0;BYSECOND=0
Timezone: Asia/Calcutta
```

## Reliability Notes

- If one sender has no qualifying email, the automation continues with the others.
- If no qualifying messages are found, it still creates a clean PDF stating no matching emails were found.
- If PDF generation fails, it retries once with a simpler layout.
- If Drive upload fails, it retries once.
- If replacement fails, it uploads a fallback file with `_retry1`.
