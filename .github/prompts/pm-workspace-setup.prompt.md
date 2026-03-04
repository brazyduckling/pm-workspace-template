---
description: "Interactive first-time setup wizard — process first meeting notes and fill context files"
---

# Setup Wizard

**IMPORTANT:** This is an interactive walkthrough. **Do not create, modify, or save any file until the user explicitly confirms.** At every step, show proposed changes and ask for permission.

## Phase 1 — Process First Meeting Notes

Start with this exact prompt to the user:

"Let's jump straight in. Paste a meeting transcript below — any meeting, real or made up, even just a few bullet points of notes."

When user provides notes:

1. Extract and show:
   - Decisions
   - Action items
   - Open questions
2. Ask: "Does this look right? Anything I missed or got wrong?"
3. Ask: "What project does this belong to? Give it a short name, like `project-alpha`."
4. Show proposed save path:
   - `docs/<project>/meeting-notes/YYYY-MM-DD-<topic>.md`
   - Explain that meeting notes live in `meeting-notes/` and date-prefix keeps sorting chronological.
   - Ask: "Want me to create this file?"
5. Show proposed project MOC:
   - `docs/<project>/<project>-moc.md`
   - Proposed entry: `- [[YYYY-MM-DD-<topic>]] — <one-line description>`
   - Explain MOC purpose as project table of contents.
   - Ask: "Want me to create this MOC?"
6. If action items exist, show proposed task additions to `ops/tasks.md`.
   - Ask: "Add these tasks?"
7. Show proposed index updates:
   - New project link in `docs/index.md`
   - New Knowledge Graph row in `AGENTS.md`
   - Ask: "Add these entries?"
8. Summarize the full pipeline in plain language:
   - raw notes → structured doc
   - routed to project folder
   - indexed in MOC
   - tasks captured
   - project registered in hub + Knowledge Graph

## Phase 2 — PRD Flow (Explain Briefly)

Explain briefly (no deep dive):
- PRDs route to `docs/<project>/prds/`
- MOC tracks PRDs in its own section
- Related docs can be connected with `[[wikilinks]]`

Ask: "Ready to fill context files, or do you want to try a PRD now?"
If user chooses PRD now, use same confirm-first pattern.

## Phase 3 — Fill Context Files

Say: "Last step — let's add your personal and org context. I'll ask a few quick questions one by one."

### Personal Context Questions
Ask one by one:
1. Job title and company
2. Team/domain
3. Manager
4. Top 1–3 goals for the next few months
5. Working style preferences

Then show complete proposed `docs/general/personal-context.md` content and ask for confirmation before saving.

### Org Context Questions
Ask one by one:
1. What the company does (one sentence)
2. Key people (name, title, domain)
3. Top 2–3 strategic priorities
4. Day-to-day tools

Then show complete proposed `docs/general/org-context.md` content and ask for confirmation before saving.

## Closing

List created/updated files and suggest next commands:
- `@workspace /session-start` for daily kickoff
- `@workspace /session-end` for daily wrap-up
- `@workspace /audit` for structural health check
