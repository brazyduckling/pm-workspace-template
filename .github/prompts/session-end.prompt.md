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

Check `inbox/` for unprocessed files. Ignore `README.md` or `.gitkeep`. Process **all** files (no selection prompt — process everything).

For each file:

### a) Distill — extract operational signals

Read the content and extract:
- **Tasks** — action items, with owner and deadline if mentioned → append to `ops/tasks.md`
- **Reminders** — time-bound follow-ups → append to `ops/reminders.md`
- **Open questions** — unresolved items needing follow-up → append to `ops/open-questions.md`

Show what was extracted. Confirm before writing to ops/ files.

### b) Route — move to permanent location

1. Determine content type and project ownership
2. Structure the content: organise into clear sections, include a **Decisions** section if decisions were made, and a **Key Context** section for important background
3. Route to the correct `docs/` location per routing rules
4. Ensure required frontmatter
5. Update relevant MOC with a `[[wikilink]]`
6. Remove the file from `inbox/`

If routing is unclear, ask the user.

## 4) Verify MOCs

Confirm docs created/updated this session are linked from a MOC.

## 5) Report

Summarise what was updated.
