---
title: "PM Workspace Template — Design Decisions & Manual"
description: "Why the template is built the way it is, and how every part of it works"
topics: ["meta", "design", "architecture"]
---

# PM Workspace Template — Design Decisions & Manual

This document explains what the template is, every significant design decision made in building it, and how to operate it. It's written for people who want to understand the system deeply — not just use it.

---

## What This Is

A boilerplate repo that turns VS Code + GitHub Copilot into a persistent, structured knowledge base for product managers.

The core problem it solves: AI assistants (ChatGPT, Copilot, Gemini) forget everything between sessions. You end up re-explaining context every time. This template gives Copilot a folder it can read as memory. Every meeting note, decision, PRD, and task you save is permanently indexed and available in every future conversation.

**On local storage:** The markdown files live on your machine. There is no automatic cloud sync, no third-party storage of the files themselves, and no background upload.

**On Copilot and data privacy:** Copilot is a cloud service. When you use `@workspace`, VS Code builds a local index of your files — but when you send a message, it includes relevant file snippets in the prompt that gets sent to GitHub's servers (backed by Azure OpenAI) for inference. File content can therefore leave your machine as part of a Copilot query, the same way any message you type into Copilot Chat does. With a **Copilot Business or Enterprise** licence, GitHub does not use your prompts or completions to train models. With an **Individual** licence, you can opt out in GitHub settings under "Copilot" → "Suggestions matching public code" and the data usage settings. Avoid pasting highly sensitive material (passwords, PII, confidential financials) until you've verified your licence terms.

---

## Key Design Decisions

### 1. Markdown files as the memory layer

**Decision:** All persistent knowledge is stored as plain `.md` files in a folder structure.

**Why:** Copilot's `@workspace` context can index and search any text file in the open VS Code folder. Markdown is human-readable, version-controllable, editable in any editor, and portable across tools (Obsidian, Notion export, any future editor). No database, no proprietary format, no lock-in.

**Trade-off considered:** A database or structured JSON schema would make queries more precise. Rejected because it would require tooling to write/read it, whereas Copilot can read raw markdown directly and the user can edit it without any interface.

---

### 2. AGENTS.md as the single instruction file

**Decision:** One master file (`AGENTS.md`) that Copilot loads at the start of every session, containing: who the user is, how the agent should behave, where things go, and what prompts exist.

**Why:** `.github/copilot-instructions.md` is auto-loaded by Copilot Chat in agent mode. It points directly to `AGENTS.md`. This means every conversation starts with full context — tone, routing rules, navigation conventions — without the user having to specify anything.

**Why not put everything in `.github/copilot-instructions.md` directly:** Copilot instruction files in `.github/` are tied to the VS Code Copilot extension. `AGENTS.md` at the root is a more visible, editable, convention-compatible pattern (mirrors `CLAUDE.md` used by Claude Code). Having it at root also makes it easy to find and edit.

---

### 3. MOC (Map of Content) pattern instead of folder scanning

**Decision:** Every `docs/` subfolder has a `<folder>-moc.md` index file. The hub is `docs/index.md`. Copilot reads the MOC first, then follows links — it does not scan directory trees.

**Why:** Without navigation files, Copilot would need to guess filenames, scan all files speculatively, or request directory listings — all of which waste context tokens and produce less reliable results. A MOC is a small file that says "here's everything in this project, what it is, and where it lives." One read → full awareness of the project's topology.

**Why not tags or file metadata:** Tags require a query layer. MOCs are readable prose that an LLM follows naturally, using the same reading patterns it was trained on.

**Implementation rule:** Every document created in `docs/` must be added to its project MOC with a `[[wikilink]]` and a one-line description. The agent enforces this automatically.

---

### 4. `[[wikilinks]]` for internal references

**Decision:** Internal cross-document references use `[[filename]]` syntax. Standard markdown `[text](url)` links are reserved for external URLs only.

**Why:** Wikilinks are short, scannable, and computable. When the agent follows a citation, it can identify it as internal vs. external by syntax alone. They also work in Obsidian if users want to visualize the graph, which several PMs do.

**Why not relative file paths (`[text](../other.md)`):** Relative paths break when files move or folders get renamed. Wikilinks are filename-stable. The agent understands both, but wikilinks create less maintenance burden.

---

### 5. Separate `ops/` from `docs/`

**Decision:** Working memory (`tasks.md`, `reminders.md`) lives in `ops/`, not inside any project folder.

**Why:** Tasks and reminders are cross-cutting. An action item from a payment domain meeting should live in the same task list as one from a courier project. If tasks were inside project folders, the agent would need to search multiple files to get a full picture. `ops/tasks.md` is always the first file read in `/session-start` — it provides a complete view of what's active, regardless of domain.

**What goes in `ops/` vs `docs/`:**
- `ops/` = working state (changes frequently, read every session, not indexed in MOCs)
- `docs/` = permanent knowledge (stable, indexed, navigable)

---

### 6. `inbox/` as a mandatory staging layer

**Decision:** All raw input (meeting notes, Slack threads, research) goes to `inbox/` first and is processed into permanent locations in a separate step.

**Why:** Immediate routing decisions made under pressure tend to be wrong. Dropping something in `inbox/` preserves it without committing to a structure. The `/session-end` prompt processes the inbox — by that point, the right project and folder are usually obvious. It also means the user can drop raw, unformatted text without the agent trying to structure it mid-conversation.

**Rule:** Nothing stays in `inbox/` across sessions. Everything gets routed or deleted at session end.

---

### 7. Four prompts, not more

**Decision:** The template ships with exactly four prompts: `/onboard`, `/session-start`, `/session-end`, `/audit`.

**Why:** A template with 10+ prompts requires the user to understand each one before they can start. Four prompts cover the full lifecycle (setup → daily start → daily end → health check) without overwhelming a new user. Additional prompts are left to the user to create — AGENTS.md instructs them to add `.prompt.md` files for any repeated task.

**Scope update:** `/onboard` was later restructured into: Orientation → transcript processing → prompt extension → personalisation → tone selection. Prompt count stayed the same (`/onboard`, `/session-start`, `/session-end`, `/audit`); only onboarding sequence changed.

**Prompts that were cut during design:**
- `/distill` — extracting decisions from notes. Merged into the `/session-end` inbox processing flow.
- `/connect` — finding links between notes. Cut because it requires human judgment on which links are meaningful; it can't be reliably automated.
- `/rethink` — challenging assumptions in a document. Useful but not a daily workflow; dropped for scope.
- `/process-meeting-notes` — dedicated meeting transcript processor. Merged into `/onboard` Phase 1 as the live demo, and into `/session-end` as part of inbox processing.

---

### 8. `/onboard` as an interactive walkthrough: orient first, then action

**Decision:** The onboarding prompt starts with a short orientation to the folder model, then runs a live transcript workflow, then teaches prompt extension, then captures personal context and tone.

**Why:** Pure action-first works well in live demos, but a boilerplate must also work for people onboarding alone without a call or recording. A 60-second map of the structure first (`docs/`, `ops/`, `inbox/`, MOCs, wikilinks, session rhythm) gives enough context for the transcript demo to make sense. Then the user sees immediate value, learns how to extend the system with custom prompts, and only then personalises it.

**Phases of the onboarding:**
1. Orient to folder structure and information flow
2. Process a transcript (demo the core mechanic)
3. Add/preview custom prompt creation (`.github/prompts/*.prompt.md`)
4. Fill personal context (make the agent useful for this specific user)
5. Pick agent tone (set a working preference that persists)

**What was removed:** The PRD mini-demo step was cut from onboarding to keep setup concise. PRD routing is still documented and follows the same mechanics (`docs/<project>/prds/` + MOC indexing).

**Transcript source:** The user can use the included example (`examples/example-meeting-transcript.md`) or paste their own. The example is a realistic customer portal redesign stakeholder meeting — specific enough to produce real output (decisions, owners, timeline) without being tied to any real company.

---

### 9. Agent tone selected during onboarding, stored in AGENTS.md

**Decision:** At the end of `/onboard`, the user picks how the agent talks to them. The choice is stored as the `Default` tone line in `AGENTS.md` and applies to all future sessions.

**Why:** Tone is a real preference — some people want blunt and fast, others want collaborative and discursive. Asking at the end of onboarding ensures it's set before day-one use. Storing it in `AGENTS.md` means it applies automatically, no reminder required.

**Three options offered:**
- Straight shooter — short, direct, no filler
- Collaborative — conversational, willing to push back, thinks with the user
- Hype machine — high energy, invested, enthusiastic

**What was cut:** "Professional & precise" was an early option. Removed because it overlaps too heavily with "Straight shooter" and was the kind of generic default that nobody would actively choose.

---

### 10. Instruction files auto-apply by glob, not by mention

**Decision:** `.github/instructions/file-routing.instructions.md` and `.github/instructions/markdown-docs.instructions.md` use `applyTo` frontmatter to auto-load whenever the agent works on matching files.

**Why:** The alternative is putting all formatting and routing rules in `AGENTS.md`. That makes AGENTS.md enormous and loads every rule for every task, even when most rules are irrelevant. Separating them out means routing rules only activate when the agent is creating or editing files in `docs/` — they don't consume context tokens during a Slack thread analysis or task update.

---

### 11. No org-context in the onboarding wizard

**Decision:** `docs/general/org-context.md` (team structure, key contacts, strategic priorities) is NOT filled in during `/onboard`.

**Why:** Personal context (role, goals, working style) is quick and introspective — the user can answer those five questions in two minutes without looking anything up. Org context is denser, requires more thought, and includes information (reporting structures, strategic priorities) that the user may not have memorized. Forcing it into a 10-minute wizard produces bad data. The file exists and is documented; the user fills it when it's useful.

---

### 12. `docs/index.md` as the only required hub

**Decision:** `docs/index.md` is the single entry point for navigating the knowledge base. AGENTS.md contains only a one-line pointer to it: "Start at `docs/index.md`."

**Earlier version:** AGENTS.md contained a full "Knowledge Graph" table listing every MOC with links. This was removed.

**Why removed:** The table duplicated information that already lived in `docs/index.md`. Two places meant two things to keep in sync, and one could drift. The one-liner pointer eliminates the duplication while keeping AGENTS.md as the definitive instruction file.

---

### 13. GitHub CLI as the default clone path

**Decision:** The README defaults to cloning with GitHub CLI (`gh repo clone`) and keeps HTTPS as fallback, with SSH setup in an optional section.

**Why:** HTTPS-first can fail for beginners when Git Credential Manager is missing (common on macOS setups using Xcode Command Line Tools git), which leads to confusing username/password prompts. SSH-first is robust but requires key generation and GitHub key setup before first use. `gh auth login` + `gh repo clone` gives a clean browser OAuth flow with fewer failure points for first-time PM users.

**Fallbacks:**
- HTTPS remains available for users who prefer plain Git.
- SSH remains available as an advanced path, documented behind a collapsible section.

---

## How the System Operates

### Session lifecycle

Every day follows three phases:

**Morning — `/session-start`**
The agent reads `ops/tasks.md` and `ops/reminders.md`. It summarises what's active and due, then asks what to work on. The user doesn't need to re-establish context — it's all there.

**During the day**
Paste raw content (meeting notes, Slack threads, decisions) directly into Copilot Chat and ask the agent to process it. Or drop files into `inbox/` and process them at the end of the day. Either path produces the same output: structured notes routed to the right project folder, tasks added to `ops/tasks.md`.

**End of day — `/session-end`**
The agent:
1. Updates `ops/tasks.md` (marks completed, adds new items from the session)
2. Updates `ops/reminders.md` (adds new time-bound items, clears passed ones)
3. Processes `inbox/` (routes each file to its permanent location, updates relevant MOC, deletes from inbox)
4. Verifies MOC coverage (anything created today should be indexed)

### How the agent navigates

When given a task, the agent:
1. Reads `docs/index.md` to understand what projects exist
2. Follows the relevant project MOC link
3. Reads the project MOC to understand the project's topology
4. Follows specific doc links from the MOC if more depth is needed
5. Acts

It never scans directories or guesses filenames. If a document isn't linked from a MOC, it is effectively invisible to the agent.

### How new documents get created

The agent always:
1. Shows the proposed file path before writing
2. Shows the content before writing
3. Asks for explicit confirmation
4. After saving: adds a `[[wikilink]]` entry to the relevant MOC
5. If it's a new project: adds the project MOC to `docs/index.md`

This confirm-before-write rule is hardcoded in AGENTS.md and enforced by all four prompts.

### How context files stay updated

`docs/general/personal-context.md` and `docs/general/org-context.md` are self-updating. When the agent detects new context in conversation (role change, new goal, new stakeholder), it:
1. Proposes the specific update
2. Asks for confirmation
3. Saves only after confirmation
4. Appends `_Last updated by Copilot: [DATE] — [what changed]_` to the file

This means context never drifts silently. Every update is visible and reversible.

---

## What to Customise First

After running `/onboard`, the most impactful customisations:

1. **Add your org context.** Open `docs/general/org-context.md` and fill in your team structure, key contacts, and current strategic priorities. This is what the agent uses when drafting stakeholder-facing content.

2. **Create a project prompt.** If you repeatedly draft the same type of document (JIRA tickets, weekly updates, stakeholder briefs), create a `.prompt.md` in `.github/prompts/`. It becomes a new `@workspace /command` immediately.

3. **Add your current projects.** If you have existing meeting notes or PRDs you want the system to know about, drop them in `inbox/` and run `/session-end` to route them.

4. **Adjust AGENTS.md.** The working principles and routing table in AGENTS.md are starting points. Edit them to match how you actually work.
