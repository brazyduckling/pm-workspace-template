# PM Knowledge Base Template

**Turn VS Code + GitHub Copilot into your personal PM knowledge base** — with persistent memory across sessions, automatic routing, and structured indexing.

> Built for the AI for PMs workshop. No prior experience with Copilot or knowledge management required.

---

## The Problem This Solves

ChatGPT and Gemini forget everything between conversations. You end up re-explaining your projects, re-pasting context, and getting generic answers.

This template gives Copilot a folder it can read as its memory. Every meeting note, decision, and task you save becomes part of its context — permanently.

**What this fixes:** re-explaining context every chat, losing action items between meetings, forgotten decisions resurfacing as surprises, context scattered across five tools, generic AI output that ignores your actual projects.

**Why not Gemini / Gems / NotebookLM?** Chat forgets. Gems have static context that goes stale. NotebookLM is read-only analysis in isolated notebooks. This tool grows automatically, tracks tasks, connects projects, and you own the files. [Full comparison ↓](#why-not-gemini--gems--notebookllm-1)

### A note on data privacy

The markdown files live on your machine — no automatic cloud sync or third-party file storage. However, Copilot is a cloud service. When you use `@workspace`, VS Code sends relevant snippets from your local files to GitHub's servers as part of the inference request. The same rules apply as for any Copilot Chat message:

- **Copilot Individual:** Data may be used to improve models by default. Opt out in GitHub Settings → Copilot.
- **Copilot Business / Enterprise:** Prompts are not used for training.

Don't paste passwords, PII, or confidential financials until you've checked your licence terms.

---

## Before Running the Agent

You'll need these installed and working. **Do this before you arrive.**

### 1. VS Code
Download and install from [code.visualstudio.com](https://code.visualstudio.com/).

### 2. GitHub account with Copilot access
- You need a **GitHub Copilot subscription** (check guild-copilot pinned post)

### 3. GitHub Copilot extension in VS Code
- Open VS Code → click the Extensions icon (left sidebar)
- Search for **GitHub Copilot**
- Click Install

### Verify it's all working
1. Open VS Code
2. Press `Cmd+Shift+P` (Mac) or `Ctrl+Shift+P` (Windows)
3. Type `Copilot: Open Chat` — a chat panel should open on the right

If the chat panel opens, you're ready.

---

## Quick Start (do this during the workshop)

**Step 1 — Download**
Click the green **Code** button at the top of this page → **Download ZIP** → unzip the folder anywhere on your computer.

**Step 2 — Open in VS Code**
Open VS Code → `File → Open Folder` → select the unzipped folder.

**Step 3 — Run the setup wizard**
Open Copilot Chat (`Cmd+Shift+I` or click the Copilot icon in the sidebar) and type:
```
/onboard
```

The wizard shows you how the workspace works by processing real meeting notes — takes about five minutes.

<details>
<summary>Advanced: Fork &amp; clone with Git</summary>

If you want to version-control your notes with Git, fork the repo first and then clone it.

**Fork the repo**
Click the **Fork** button at the top of this page. This creates your own copy under your GitHub account.

**Option A — GitHub CLI**

Install from [cli.github.com](https://cli.github.com/) or with Homebrew:

```bash
brew install gh
```

Authenticate (one-time):

```bash
gh auth login
```

Clone your fork:

```bash
gh repo clone <your-username>/pm-workspace-template
```

**Option B — HTTPS**

You'll need Git installed first: [git-scm.com/downloads](https://git-scm.com/downloads). Most Macs already have it — run `git --version` in Terminal to check.

```bash
git clone https://github.com/<your-username>/pm-workspace-template.git
```

**Option C — SSH**

Generate a new key:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Start the ssh-agent:

```bash
eval "$(ssh-agent -s)"
```

Add the key:

```bash
ssh-add ~/.ssh/id_ed25519
```

Copy the public key and add it in GitHub:

```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

GitHub path: Settings → SSH and GPG keys → New SSH key.

Then clone with SSH:

```bash
git clone git@github.com:<your-username>/pm-workspace-template.git
```

Open VS Code → `File → Open Folder` → select the cloned folder.

</details>

---

## After the Workshop — Daily Habits

**Every morning:**
```
/session-start
```
Copilot reads your tasks, reminders, and open questions and tells you what's on your plate.

**During the day:**
Drop files into `inbox/`, then run:
```
/process
```
Copilot extracts tasks and open questions to `ops/`, then routes the content to its permanent location. Originals are preserved in `archive/` for deeper reference. You choose which files to process.

**End of day:**
```
/session-end
```
Copilot updates your tasks, processes your inbox, and makes sure everything is indexed.

**Periodically:**
```
/audit
```
Checks that all your docs are linked from a MOC, no broken links, everything properly structured.

---

## Core Concepts

| Concept | What it is |
|---|---|
| **AGENTS.md** | The AI's instruction manual. Tells Copilot who you are, how to behave, and where things go. Loaded automatically every session. Also where the agent's name (**Wibby**, short for Weaver) is defined. |
| **MOC** | Map of Content. An index file per project — lists every doc with a link and one-line description. The AI reads this instead of scanning folders. |
| **`[[wikilinks]]`** | How notes connect to each other. Write `[[filename]]` to link. The AI follows these connections for context. |
| **`ops/`** | Working memory. `tasks.md`, `reminders.md`, and `open-questions.md` — updated every session. |
| **`inbox/`** | Drop zone for raw input. Files here get routed to the right place. |
| **`archive/`** | Storage for raw originals after processing. Preserved for deeper reference — only accessed on request. |
| **Prompt files** | Reusable AI commands saved in `.github/prompts/`. Invoke with `/name`. |

---

## Folder Structure

```
├── AGENTS.md                       ← AI's instruction manual
├── .github/
│   ├── copilot-instructions.md     ← Points Copilot to AGENTS.md
│   ├── instructions/               ← Auto-loaded formatting + routing rules
│   └── prompts/                    ← Your AI commands (/onboard, /session-start, etc.)
├── docs/
│   ├── index.md                    ← Hub linking all your projects
│   └── general/
│       ├── personal-context.md     ← Your role, goals, preferences
│       └── org-context.md          ← Your org, key contacts, strategy
├── ops/
│   ├── tasks.md                    ← Active work items
│   ├── reminders.md                ← Time-bound follow-ups
│   └── open-questions.md           ← Unresolved questions across projects
├── inbox/                          ← Drop raw files here
└── archive/                        ← Raw originals preserved after processing
```

---

## Adding a New Project

When you start working on something new:

1. Create `docs/<project-name>/` folder
2. Create `docs/<project-name>/<project-name>-moc.md` (the project's index)
3. Add a link in `docs/index.md` under Project Areas

Meeting notes go to `docs/<project-name>/meeting-notes/`. PRDs go to `prds/`.

---

## Troubleshooting

**"Copilot says it can't find my files"**
Make sure you opened the *folder* in VS Code, not just individual files. `File → Open Folder` → select the repo root.

**"/onboard doesn't work"**
Make sure you opened the *folder* in VS Code (`File → Open Folder`), not just an individual file. Copilot needs access to the full folder to run prompt commands.

**"Copilot is ignoring AGENTS.md"**
Check that `.github/copilot-instructions.md` exists and contains the pointer line. This file is what makes Copilot load AGENTS.md automatically.

---

## Optional: Obsidian

Open this folder as an [Obsidian](https://obsidian.md/) vault to visualize your knowledge graph and navigate via `[[wikilinks]]`. Not required — everything works in VS Code alone.

---

## Why not Gemini / Gems / NotebookLM?

| | Gemini Chat | Gemini Gems | NotebookLM | This tool |
|---|---|---|---|---|
| **Memory between sessions** | None — starts from zero | Static — you write it once, it goes stale | Per-notebook only — siloed | Dynamic — grows every time you work |
| **Context updates** | Manual re-pasting | Manual rewriting | Re-upload files | Automatic — every processed note adds to it |
| **Task tracking** | No | No | No | Yes — extracted from meetings, checked daily |
| **Cross-project awareness** | No | No | No — each notebook is isolated | Yes — one workspace, all projects connected |
| **Structured routing** | No | No | No | Yes — inbox → docs → archive, auto-indexed |
| **You own the files** | No — cloud only | No — cloud only | No — cloud only | Yes — plain markdown on your machine |
