---
description: "End a working session — persist progress and maintain the system"
---

Perform end-of-session maintenance:

## 1) Update Tasks

In `ops/tasks.md`:
- Mark completed items as done (`- [x]`)
- Add new tasks from this session using the format: `- [ ] **[Project]** Task description — _due: DD MMM YYYY_ · _owner: Name_`
- Note blockers for stuck items

## 2) Update Reminders

In `ops/reminders.md`:
- Add new time-bound follow-ups using the format: `- [ ] **DD MMM YYYY** — **[Project]** Description`
- Mark actioned reminders as done (`- [x]`)

## 3) Archive Completed Ops

Scan `ops/tasks.md`, `ops/reminders.md`, and `ops/open-questions.md` for `[x]` items.

For each `[x]` item:
- Confirm it has a `**[Project]**` tag. If missing, infer from context or ask the user.
- Collect the completion date (use today's date if not specified).
- For questions specifically: ask the user for the answer/resolution text and who provided it before archiving.

Then:
1. Append each item to the appropriate monthly file in `ops/done/`:
   - Tasks → `ops/done/YYYY-MM-tasks.md`
   - Reminders → `ops/done/YYYY-MM-reminders.md`
   - Questions → `ops/done/YYYY-MM-questions.md`
2. If the monthly file doesn't exist, create it using the template below.
3. If this is the first entry in a new monthly file, add it to the relevant section of `ops/done/done-index.md` as `[[YYYY-MM-tasks]]`, `[[YYYY-MM-reminders]]`, or `[[YYYY-MM-questions]]`.
4. Remove the `[x]` items from the active ops files.

### Monthly file templates

**`ops/done/YYYY-MM-tasks.md`**
```
# Tasks Done — Month YYYY

<!-- Items moved here from ops/tasks.md during /session-end. Do not edit manually. -->

- [x] **[Project]** Task description
  _Added: DD MMM YYYY · Completed: DD MMM YYYY_
```

**`ops/done/YYYY-MM-reminders.md`**
```
# Reminders Done — Month YYYY

<!-- Items moved here from ops/reminders.md during /session-end. Do not edit manually. -->

- [x] **[Project]** Description
  _Due: DD MMM YYYY · Completed: DD MMM YYYY_
```

**`ops/done/YYYY-MM-questions.md`**
```
# Questions Resolved — Month YYYY

<!-- Items moved here from ops/open-questions.md during /session-end. Do not edit manually. -->

- [x] **[Project]** Question text
  _Asked: YYYY-MM-DD · Resolved: DD MMM YYYY_
  **Answer:** Resolution text — *answered by [person]*
```

Show the user a summary of what was archived before removing items from the active files. Confirm before writing.

## 4) Process Inbox

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
5. Add `source: "[[archived-filename]]"` to the new file's frontmatter
6. Update relevant MOC with a `[[wikilink]]`
7. **Archive the original:**
   1. Rename it to a descriptive title with date prefix (e.g., `2026-03-12-raw-kickoff-transcript.md`)
   2. Move to `archive/<project>/` (create the folder if it doesn't exist)
   3. If this is the first file in `archive/<project>/`: create `<project>-archive-moc.md` and add it to `archive/archive-index.md`
   4. Add a `[[wikilink]]` entry to `archive/<project>/<project>-archive-moc.md`

If routing is unclear, ask the user.

## 5) Verify MOCs

Confirm docs created/updated this session are linked from a MOC.

## 6) Report

Summarise what was updated, including a count of ops items archived (e.g., "3 tasks, 1 reminder, 2 questions moved to ops/done/").
