# AGENTS.md
<!-- Last updated: 10 Mar 2026 -->

## Who I Am

**[Your Role]** at **[Your Company]**.

## Current Context

- **Domain / Team:** [Your current team or domain]
- **Manager:** [Your manager's name]
- **Key projects:** [List active projects]

## How I Work

### Tone & Audience

- **Stakeholder-facing**: concise, outcome-focused, business language
- **Technical**: precise, no ambiguity, acceptance-criteria style
- **Personal**: honest, structured, action-oriented
- **Default**: direct, professional, no filler <!-- set during /onboard — update this line to change agent tone -->

### Working Principles

1. **No hallucination.** Use only provided info. Mark missing items as `TBD`.
2. **Structure over prose.** Prefer headings, bullets, and tables.
3. **Suggest next steps.** End with practical next actions.
4. **MOC-first navigation.** Read MOCs first, then follow `[[wikilinks]]` as needed.
5. **Maintain indexes.** After creating/updating files in `docs/`, update the relevant MOC.
6. **Inbox-first capture.** Raw content goes to `inbox/` first. Direct updates allowed only for `ops/tasks.md`, `ops/reminders.md`, and `ops/open-questions.md`.

### Session Rhythm

1. **Orient** (`@workspace /session-start`)
   - Read `ops/tasks.md`, `ops/reminders.md`, and `ops/open-questions.md`
   - Summarize status and ask what to work on
2. **Work**
   - Capture raw content in `inbox/`
   - Run `@workspace /process` to extract tasks, reminders, and open questions, then route content to permanent locations
3. **Persist** (`@workspace /session-end`)
   - Update tasks and reminders
   - Process remaining inbox files (extract ops signals, then route)
   - Update MOCs

### Memory Type Routing

| What you captured | Where it goes |
|---|---|
| Meeting notes | `docs/<project>/meeting-notes/` |
| PRD or spec | `docs/<project>/prds/` |
| Task / action item | `ops/tasks.md` |
| Time-bound follow-up | `ops/reminders.md` |
| Open question | `ops/open-questions.md` |
| Raw unprocessed input | `inbox/` |
| Cross-project / org context | `docs/general/` |

## Navigation

Start at `docs/index.md` — it links to all project MOCs and ops files.

`docs/general/design-decisions.md` is a reference doc. Read it only for meta-questions about how or why the workspace template is designed, not for normal daily session execution.

### Adding a New Project

1. Create `docs/<project-name>/` and `<project-name>-moc.md`
2. Add the MOC to `docs/index.md`
3. Route docs by type (`meeting-notes/`, `prds/`)

## Conventions

- Use `[[wikilinks]]` for internal references
- Use standard markdown links for external URLs
- Every `docs/` subfolder has a `<folder>-moc.md`
- `ops/` is working memory
- `inbox/` is temporary staging
- `docs/index.md` is the hub MOC

## Self-Maintenance Protocol

### When to Update

- New project added
- Role/team context changed
- Routing conventions changed
- Docs created/moved/archived in `docs/`

### How to Update

- Update MOCs and AGENTS.md directly for routine maintenance
- Update the date in this file's header comment

### Self-Updating Context Files

These files always require confirmation before writing updates:

| File | Triggers |
|---|---|
| `docs/general/personal-context.md` | Role change, goal updates, working-style preferences |
| `docs/general/org-context.md` | New key contact, org change, strategy updates |

Protocol:
1. Detect new context in conversation
2. Propose update
3. Ask for confirmation
4. Save only after confirmation

## Prompt Files

| Prompt | Purpose |
|---|---|
| `/onboard` | Interactive first-time onboarding |
| `/session-start` | Daily orient flow |
| `/session-end` | Daily persist/cleanup flow |
| `/process` | Extract tasks, reminders, and open questions from inbox files, then route to permanent locations |
| `/audit` | Structure and indexing audit |
| `/personalize` | Set personal context — role, team, goals, working style |

## Design Philosophy

1. The vault is the memory.
2. MOCs reduce search cost and keep context discoverable.
3. Wikilinks encode relationships across notes.
4. Regular maintenance prevents drift.
5. Full rationale and trade-offs live in `docs/general/design-decisions.md` (meta reference).
