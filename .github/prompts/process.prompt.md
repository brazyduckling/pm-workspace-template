---
description: "Process inbox files — extract tasks, reminders, and open questions, then route content to its permanent location"
---

# Process Inbox

## 1) Check Inbox

Read `inbox/` for files. Ignore `README.md` or `.gitkeep`.

- If **no files found**: say "Inbox is empty. Drop files in `inbox/` or paste content into chat and I'll save it there for processing."
- If **files found**: list them by name and ask:

> "Process all of these, or pick specific files?"

Wait for the user's answer. Proceed only with selected files.

## 2) For Each File — Distill

Read the file content and extract operational signals:

### Extraction targets

- **Tasks** — action items, with owner and deadline if mentioned
- **Reminders** — time-bound follow-ups (has a specific date or timeframe)
- **Open questions** — unresolved items that need follow-up or a decision

Show the extraction grouped by type. Then ask:

> "Add these to ops? ([N] tasks → `ops/tasks.md`, [N] reminders → `ops/reminders.md`, [N] open questions → `ops/open-questions.md`)"

Wait for confirmation before writing to any ops/ file.

- Tasks: append to `ops/tasks.md` under `## Active`
- Reminders: append to `ops/reminders.md`
- Open questions: append to `ops/open-questions.md`

If nothing was extracted for a category, skip it silently.

## 3) For Each File — Route

Determine the content type and project, then route to its permanent location in `docs/`.

1. **Determine project.** If unclear, ask the user.
2. **Determine content type** per the routing rules in `file-routing.instructions.md` (meeting notes, PRD, cross-project context, etc.).
3. **Structure the content.** When routing raw or semi-structured content (transcripts, notes), organise it into clear sections. Include a **Decisions** section if any decisions were made, and a **Key Context** section for important background or constraints worth preserving.
4. **Add required frontmatter** per `markdown-docs.instructions.md`.
5. **Show the user:**
   - Proposed file path
   - Proposed structured content (in a code block)
   - Proposed MOC entry (`[[wikilink]]` + one-line description)
6. **Ask for confirmation** before writing.
7. After confirmation:
   - Create the file in `docs/<project>/<type>/`
   - Add the `[[wikilink]]` entry to the project's MOC
   - If this is a new project: create the MOC and add it to `docs/index.md`
   - Add `source: "[[archived-filename]]"` to the new file's frontmatter
   - **Archive the original:**
     1. Rename it to a descriptive title with date prefix (e.g., `2026-03-12-raw-kickoff-transcript.md`)
     2. Move to `archive/<project>/` (create the folder if it doesn't exist)
     3. If this is the first file in `archive/<project>/`: create `<project>-archive-moc.md` and add it to `archive/archive-index.md`
     4. Add a `[[wikilink]]` entry to `archive/<project>/<project>-archive-moc.md`

## 4) Report

After all files are processed, summarise:
- What was added to ops/ (tasks, reminders, open questions)
- What was routed and where
- Any files skipped or still in inbox
