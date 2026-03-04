---
description: "Interactive first-time setup wizard — process first meeting notes and fill context files"
---

# Setup Wizard

**IMPORTANT:** This is an interactive walkthrough. **Do not create, modify, or save any file until the user explicitly confirms.** At every step, show proposed changes and ask for permission.

Start by saying:

> **Welcome to your PM knowledge base.**
>
> This workspace is a structured folder of markdown files that gives me — your AI assistant — persistent memory across sessions. Everything you drop here (meeting notes, PRDs, decisions, tasks) gets indexed so I can find and use it in future conversations.
>
> I'm going to walk you through how it works by doing something real together. It takes about **10 minutes**. Ready? Let's go.

## Phase 1 — Process First Meeting Notes

Ask the user:

> We'll start by processing a meeting transcript. You have two options:
>
> **A)** Use the example transcript included in this repo — it's a stakeholder alignment meeting about a customer portal redesign. You can find it at `examples/example-meeting-transcript.md`.
>
> **B)** Paste your own meeting notes — any real or made-up meeting, even just a few bullet points.
>
> Which do you prefer — **A** or **B**?

If the user picks A, read `examples/example-meeting-transcript.md` and use that as the input.
If the user picks B, say: "Go ahead — paste your notes below."

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
7. Show proposed index update:
   - New project link in `docs/index.md`
   - Ask: "Add this to the hub?"
8. Summarize the full pipeline in plain language:
   - raw notes → structured doc
   - routed to project folder
   - indexed in MOC
   - tasks captured
   - project registered in the hub index

## Phase 2 — PRD Flow (Explain Briefly)

Explain briefly (no deep dive):
- PRDs route to `docs/<project>/prds/`
- MOC tracks PRDs in its own section
- Related docs can be connected with `[[wikilinks]]`

Ask: "Ready to fill context files, or do you want to try a PRD now?"
If user chooses PRD now, use same confirm-first pattern.

## Phase 3 — Fill Context Files

Say: "Last step — let's add some context about you so the AI knows who it's working with."

### Personal Context Questions
Ask one by one:
1. Job title and company
2. Team/domain
3. Manager
4. Top 1–3 goals for the next few months
5. Working style preferences

Then show complete proposed `docs/general/personal-context.md` content and ask for confirmation before saving.

## Closing

List all files created/updated during setup.

Then present the available commands:

> **Your commands:**
>
> | Command | What it does |
> |---|---|
> | `@workspace /session-start` | Reads your tasks and reminders, tells you what's active, asks what to work on |
> | `@workspace /session-end` | Updates tasks, processes your inbox, makes sure everything is indexed |
> | `@workspace /audit` | Checks structural health — missing MOCs, orphan docs, broken links |
>
> **You can create your own commands too.** Add a `.prompt.md` file to `.github/prompts/` and it becomes a new `@workspace /command`. Your prompts can even call each other — chain them into workflows.
>
> **The key thing to remember:** the AI has access to everything you put in this workspace — but only what you put here. Meeting notes, PRDs, Slack threads, research — drop it in `inbox/` and ask the agent to process it. Or paste it straight into chat. The more context you feed it, the smarter it gets.
>
> Go wild. Build prompts for weekly updates, ticket drafts, stakeholder briefs — whatever you do repeatedly. This is your system now.
