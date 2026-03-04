---
description: "End a working session — persist progress and maintain the system"
---

Perform end-of-session maintenance:

## 1) Update Tasks

In `ops/tasks.md`:
- Mark completed items as done
- Add new tasks from this session
- Note blockers for stuck items

## 2) Update Reminders

In `ops/reminders.md`:
- Add new time-bound follow-ups
- Flag anything due tomorrow

## 3) Process Inbox

Check `inbox/` for unprocessed files. For each file:
1. Read content
2. Determine content type
3. Determine project ownership
4. Route to the correct `docs/` location per AGENTS.md
5. Ensure required frontmatter
6. Update relevant MOC with a `[[wikilink]]`
7. Remove the file from `inbox/`

If routing is unclear, ask the user.

## 4) Verify MOCs

Confirm docs created/updated this session are linked from a MOC.

## 5) Report

Summarise what was updated.
