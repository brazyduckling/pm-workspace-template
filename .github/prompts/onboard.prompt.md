---
description: "Interactive first-time onboarding — learn how the workspace works by doing something real"
---

# Onboarding

**IMPORTANT:** This is an interactive walkthrough. **Do not create, modify, or save any file until the user explicitly confirms.** At every step, show proposed changes and ask for permission.

Start by saying:

> **Okay. I'm going to show you something.**
>
> This folder is a structured knowledge base. I can read it, write to it, and navigate it like a codebase. Every meeting, decision, PRD, and task you put here is permanently indexed — and I can find it in any future conversation.
>
> No more re-explaining your projects. No more pasting context into every chat. It's just there, every time.
>
> One thing worth knowing: **everything stays local.** These are just markdown files on your machine. Nothing gets sent anywhere, nothing is stored in the cloud. It's yours.
>
> We're going to set it up right now, live, with real content. Ten minutes. Let's go.

## Phase 1 — Process Your First Meeting Notes

Say:

> "Here's what we're doing: I'm going to take a meeting transcript, pull out the decisions, action items, and open questions, then save it as a structured note in the right folder, add it to the project index, and drop any tasks into your task list. All confirmed step by step before anything gets written."
>
> "Ready? You've got two options:"
>
> **A — Use the example transcript.** There's a stakeholder meeting already in the repo at `examples/example-meeting-transcript.md`. Use this if you just want to watch it work.
>
> **B — Use your own notes.** Paste anything — rough, bullet points, whatever.
>
> Which one?

Wait for the user to respond before continuing. Do not use the ask_questions tool.

If the user picks A, read `examples/example-meeting-transcript.md` and use it as input. Say: "Good. That one's a solid example — watch what happens."

If the user picks B, say: "Paste it. Rough is fine."

When you have the notes, say:

> "Here's what I pulled out:"

Then show:
- **Decisions** — things that got agreed
- **Action items** — with owner and deadline if mentioned
- **Open questions** — still unresolved

Ask: "Anything I missed or got wrong?"

Wait for confirmation, then:

1. Ask: "What project does this belong to? Short name — like `customer-portal` or `q2-roadmap`."

2. Show the exact file path you'd save to:
   > `docs/<project>/meeting-notes/YYYY-MM-DD-<topic>.md`
   >
   > Meeting notes live inside the project folder. Date prefix = chronological order, always.

   Ask: "Create this file?"

3. Show the project MOC you'd create:
   > `docs/<project>/<project>-moc.md`
   >
   > This is the project's index. Every doc gets listed here with a `[[wikilink]]` and a one-liner. I read this one file and immediately know what exists. This is how I navigate — not by scanning folders.

   Show the entry: `- [[YYYY-MM-DD-<topic>]] — <one-line description>`

   Ask: "Create the MOC?"

4. If there are action items, show what you'd add to `ops/tasks.md`:
   > Your task list. First thing I read every session. Every action item from every meeting ends up here.

   Ask: "Add these tasks?"

5. Show the hub update:
   > One line in `docs/index.md` linking to the new project MOC. Without this, the project doesn't exist to me.

   Ask: "Add it?"

6. After all confirmations, narrate what just happened:

   > "That's it. One messy transcript → structured note in the right folder, indexed in a MOC, action items captured, project registered in the hub.
   >
   > Every future session, I know this conversation happened. That's the whole thing. That's what this system does."

## Phase 2 — PRD Flow (Quick)

Say:

> "Same system, different folder. PRDs go to `docs/<project>/prds/`. MOC tracks them separately. You can link a PRD back to the meeting that created it — full traceable thread from conversation to spec."

Ask: "Want to run a PRD through it now, or keep moving?"

If yes, same confirm-first flow. If no, move on.

## Phase 3 — Tell Me About You

Say:

> "Last thing. Five questions. I need context to be useful."

Ask one by one, waiting for each answer:
1. "Job title. Where do you work?"
2. "What team or domain are you in?"
3. "Who's your manager?"
4. "Top 1–3 goals for the next few months?"
5. "How do you work? Fast-paced, async-first, whatever's true."

Show the full proposed `docs/general/personal-context.md`. Ask: "Save this?"

Wait for confirmation before saving.

## Closing

List every file created during setup.

Then say:

> "Done. Three commands worth knowing:"
>
> | Command | What it does |
> |---|---|
> | `@workspace /session-start` | Reads your tasks and reminders, tells you what's happening, asks what to work on |
> | `@workspace /session-end` | Updates tasks, processes inbox, makes sure everything is indexed |
> | `@workspace /audit` | Structural check — missing MOCs, orphan docs, broken links |
>
> **You can build your own.** Drop a `.prompt.md` in `.github/prompts/` and it becomes a new `@workspace /command`. Weekly update, ticket draft, stakeholder brief — whatever you do repeatedly, make a prompt for it.
>
> **Only rule:** I know what's in this folder. Nothing else. Meeting notes, Slack threads, research — drop it in `inbox/` or paste it into chat. That's how you feed me context.
>
> This is your system. Use it.

---

## Final Step — Pick Your Agent Tone

Say:

> "One thing left. How do you want me to talk to you? Not for external docs — just when we're working."
>
> **A — Straight shooter.** Short, blunt, no fluff. You ask, I answer. Fast.
>
> **B — Collaborative partner.** Conversational but sharp. I'll push back when something's off. Think with you, not just for you.
>
> **C — Hype machine.** High energy. I'm invested in what you're building and I won't hide it.
>
> Which one?

Wait for the user to respond before continuing. Do not use the ask_questions tool.

Then:
- Update the `## How I Work → Tone & Audience → Default` line in `AGENTS.md` to reflect their choice.
- Confirm in one line:
  - Straight shooter: "Done. Short and direct from here."
  - Collaborative partner: "Done. I'll think with you."
  - Hype machine: "Done. Let's build something."
- Ask for confirmation before saving.

