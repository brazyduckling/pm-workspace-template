# PM Knowledge Base Template

**Turn VS Code + GitHub Copilot into your personal PM knowledge base** — with persistent memory across sessions, automatic routing, and structured indexing.

> Built for the AI for PMs workshop. No prior experience with Copilot or knowledge management required.

---

## The Problem This Solves

ChatGPT and Gemini forget everything between conversations. You end up re-explaining your projects, re-pasting context, and getting generic answers.

This template gives Copilot a folder it can read as its memory. Every meeting note, decision, and task you save becomes part of its context — permanently.

---

## Before the Workshop

You'll need these installed and working. **Do this before you arrive.**

### 1. VS Code
Download and install from [code.visualstudio.com](https://code.visualstudio.com/).

### 2. GitHub account with Copilot access
- You need a **GitHub Copilot subscription** (Individual: $10/mo).
- If you don't have one, start a free trial at [github.com/features/copilot](https://github.com/features/copilot).

### 3. GitHub Copilot extension in VS Code
- Open VS Code → click the Extensions icon (left sidebar)
- Search for **GitHub Copilot**
- Click Install

### 4. Git
Download from [git-scm.com](https://git-scm.com/downloads). Most Macs already have it — run `git --version` in Terminal to check.

### Verify it's all working
1. Open VS Code
2. Press `Cmd+Shift+P` (Mac) or `Ctrl+Shift+P` (Windows)
3. Type `Copilot: Open Chat` — a chat panel should open on the right

If the chat panel opens, you're ready.

---

## Quick Start (do this during the workshop)

**Step 1 — Fork this repo**
Click the **Fork** button at the top of this page. This creates your own copy to customize.

**Step 2 — Clone it to your computer**
```bash
git clone https://github.com/<your-username>/pm-workspace-template
```

**Step 3 — Open in VS Code**
Open VS Code → `File → Open Folder` → select the folder you just cloned.

**Step 4 — Run the setup wizard**
Open Copilot Chat (`Cmd+Shift+I` or click the Copilot icon in the sidebar) and type:
```
@workspace /pm-workspace-setup
```

The wizard will guide you through everything interactively — paste a meeting transcript, see how it gets routed and indexed, then fill in your personal and org context.

---

## After the Workshop — Daily Habits

**Every morning:**
```
@workspace /session-start
```
Copilot reads your tasks and reminders and tells you what's on your plate.

**During the day:**
Paste raw notes into Copilot Chat and ask it to extract decisions and action items. Or drop files into `inbox/` — they'll get routed when you run session-end.

**End of day:**
```
@workspace /session-end
```
Copilot updates your tasks, processes your inbox, and makes sure everything is indexed.

**Periodically:**
```
@workspace /audit
```
Checks that all your docs are linked from a MOC, no broken links, everything properly structured.

---

## Core Concepts

| Concept | What it is |
|---|---|
| **AGENTS.md** | The AI's instruction manual. Tells Copilot who you are, how to behave, and where things go. Loaded automatically every session. |
| **MOC** | Map of Content. An index file per project — lists every doc with a link and one-line description. The AI reads this instead of scanning folders. |
| **`[[wikilinks]]`** | How notes connect to each other. Write `[[filename]]` to link. The AI follows these connections for context. |
| **`ops/`** | Working memory. `tasks.md` and `reminders.md` — updated every session. |
| **`inbox/`** | Drop zone for raw input. Files here get routed to the right place. |
| **Prompt files** | Reusable AI commands saved in `.github/prompts/`. Invoke with `@workspace /name`. |

---

## Folder Structure

```
├── AGENTS.md                       ← AI's instruction manual
├── .github/
│   ├── copilot-instructions.md     ← Points Copilot to AGENTS.md
│   ├── instructions/               ← Auto-loaded formatting + routing rules
│   └── prompts/                    ← Your AI commands (/pm-workspace-setup, /session-start, etc.)
├── docs/
│   ├── index.md                    ← Hub linking all your projects
│   └── general/
│       ├── personal-context.md     ← Your role, goals, preferences
│       └── org-context.md          ← Your org, key contacts, strategy
├── ops/
│   ├── tasks.md                    ← Active work items
│   └── reminders.md                ← Time-bound follow-ups
└── inbox/                          ← Drop raw files here
```

---

## Adding a New Project

When you start working on something new:

1. Create `docs/<project-name>/` folder
2. Create `docs/<project-name>/<project-name>-moc.md` (the project's index)
3. Add a link in `docs/index.md` under Project Areas

Meeting notes go to `docs/<project-name>/meeting-notes/`. PRDs go to `prds/`. Decisions to `decisions/`.

---

## Troubleshooting

**"Copilot says it can't find my files"**
Make sure you opened the *folder* in VS Code, not just individual files. `File → Open Folder` → select the repo root.

**"/pm-workspace-setup doesn't work"**
Make sure to type `@workspace` before the command: `@workspace /pm-workspace-setup`. The `@workspace` tells Copilot to read your files.

**"Copilot is ignoring AGENTS.md"**
Check that `.github/copilot-instructions.md` exists and contains the pointer line. This file is what makes Copilot load AGENTS.md automatically.

---

## Optional: Obsidian

Open this folder as an [Obsidian](https://obsidian.md/) vault to visualize your knowledge graph and navigate via `[[wikilinks]]`. Not required — everything works in VS Code alone.
