# PM Knowledge Base Template

A ready-to-use workspace that turns GitHub Copilot in VS Code into a PM assistant with persistent memory across sessions.

## What This Is

A folder of markdown files with instruction files that tell Copilot:
- where to put things (meeting notes, PRDs, decisions, tasks)
- how to format them (frontmatter, wikilinks, naming)
- how to navigate them (MOCs / Maps of Content)
- how to keep structure healthy (audit checks)

The folder is the memory. Copilot does not keep memory between sessions by itself.

## Prerequisites

Before the workshop, make sure you have:
- VS Code installed
- GitHub Copilot access
- GitHub Copilot extension installed in VS Code
- Git installed

## Quick Start

1. Fork this repository.
2. Open it as a folder in VS Code.
3. Open Copilot Chat and run `@workspace /setup`.
4. Follow the interactive onboarding flow.

The wizard takes you through:
- processing a first meeting transcript
- understanding routing + MOCs
- filling personal and org context

## Daily Workflow

- Start of day: `@workspace /session-start`
- End of day: `@workspace /session-end`
- Periodically: `@workspace /audit`

## Core Concepts

| Concept | What it is |
|---|---|
| AGENTS.md | Instruction manual for Copilot in this workspace |
| MOC | Map of Content: index file for each area/project |
| `[[wikilinks]]` | Internal links connecting notes and documents |
| `ops/` | Working memory (`tasks.md`, `reminders.md`) |
| `inbox/` | Staging area for raw inputs |
| Prompt files | Reusable interactive workflows in `.github/prompts/` |

## Adding a New Project

1. Create `docs/<project-name>/`.
2. Create `docs/<project-name>/<project-name>-moc.md`.
3. Add it to `docs/index.md`.
4. Add it to the Knowledge Graph table in `AGENTS.md`.

Meeting notes should go to `docs/<project-name>/meeting-notes/`.

## Folder Structure

- `AGENTS.md` — AI behavior + structure rules
- `.github/copilot-instructions.md` — bridge that points Copilot to AGENTS.md
- `.github/instructions/` — formatting + routing rules
- `.github/prompts/` — interactive prompt workflows
- `docs/` — knowledge base + MOCs
- `ops/` — tasks and reminders
- `inbox/` — temporary raw capture

## Optional

This structure is compatible with Obsidian if you also want graph visualization.
