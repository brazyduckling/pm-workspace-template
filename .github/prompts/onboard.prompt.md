---
description: "Interactive first-time onboarding — learn how the workspace works by doing something real"
---

# Onboarding

**IMPORTANT:** This is an interactive walkthrough. **Do not create, modify, or save any file until the user explicitly confirms.** At every step, show proposed changes and ask for permission.

Start by saying:

> Welcome. You've set up a structured markdown workspace that gives me persistent memory across sessions. No more repeating context. Everything you add gets indexed for future use.
>
> I'll show you how it works by processing a meeting transcript. Takes about 10 minutes. You'll end up with a working knowledge base.

## Phase 1 — Process Your First Meeting Notes

This is the core part. Let's use the system.

Present these two options as a selection for the user to pick from:

- **Use the example transcript** — there's a ready-made stakeholder meeting about a customer portal redesign waiting for you at `examples/example-meeting-transcript.md`. Perfect if you want to jump straight in.
- **Use my own notes** — paste anything: a real meeting, a made-up one, even just a few bullet points. It all works.

Wait for the user to pick before continuing.

If the user picks the example, read `examples/example-meeting-transcript.md` and use it as input. Say: "Good choice. Let me process it."

If the user picks their own, say: "Paste your notes below."

When you have the notes, before doing anything else, narrate what you're seeing:

> Here's what I extracted:

Then show:
- **Decisions** — things that got agreed
- **Action items** — things someone needs to do (with owner and deadline if mentioned)
- **Open questions** — stuff that's still unresolved

Ask: "Does this look right? Anything I missed or got wrong?"

Wait for confirmation, then:

1. Ask: "What project does this belong to? Give it a short name — like `customer-portal` or `q2-roadmap`."

2. Show the exact file path you'd save to:
   > `docs/<project>/meeting-notes/YYYY-MM-DD-<topic>.md`
   >
   > Meeting notes live in `meeting-notes/` inside the project folder. Date prefix keeps everything sorted chronologically — you can scroll back through weeks of meetings in order.

   Ask: "Want me to create this?"

3. Show the project MOC you'd create:
   > `docs/<project>/<project>-moc.md`
   >
   > This is your project's table of contents. Every doc in this project gets listed here with a `[[wikilink]]` and a one-liner. Instead of scanning folders, I just read this file and instantly know what's here. It's tiny but it's the whole magic of the system.

   Show the entry: `- [[YYYY-MM-DD-<topic>]] — <one-line description>`

   Ask: "Want me to create this MOC?"

4. If there are action items, show what you'd add to `ops/tasks.md`:
   > This is your task list. It's the first thing I read every morning when you run `/session-start`. Any action item from any meeting goes here.

   Ask: "Add these tasks?"

5. Show the hub update:
   > I'd add a line to `docs/index.md` linking to the new project MOC. This is how I know the project exists. Without this, it's invisible to me.

   Ask: "Add this to the hub?"

6. After all confirmations, narrate what just happened:

   > One messy transcript became a clean structured note, saved in the right folder, indexed in a MOC, action items in your task list, project registered in the hub. Every future session, I'll know this conversation happened.
   >
   > That's the system. It does this for every note, PRD, or doc you add.

## Phase 2 — Quick PRD Preview (No Action Needed)

Say:

> PRDs work similarly but route to prds/.

Explain briefly:
- PRDs go to `docs/<project>/prds/` instead of `meeting-notes/`
- MOC tracks them separately under a `## PRDs` section
- You can link a PRD back to the meeting that inspired it using `[[wikilinks]]` — so there's a traceable thread from conversation → decision → spec

Ask: "Want to try a PRD now, or shall we move on?"

If yes, run it with the same confirm-first pattern. If no, move on.

## Phase 3 — Tell Me About You

Say:

> Last step: context about you so I can be useful. Five quick questions, one at a time.

Ask one by one, waiting for each answer:
1. "What's your job title and where do you work?"
2. "What team or domain are you in right now?"
3. "Who's your manager?"
4. "What are your top 1–3 goals for the next few months?"
5. "How do you like to work? (e.g. async-first, fast-paced, data-driven, whatever fits)"

Then show the full proposed `docs/general/personal-context.md` and ask: "Happy with this? Shall I save it?"

Wait for confirmation before saving.

## Closing

First, list every file created during setup.

Then say:

> You're set up. Here's your toolkit:

> | Command | What it does |
> |---|---|
> | `@workspace /session-start` | Morning kickoff — reads your tasks and reminders, tells you what's going on, asks what you want to work on |
> | `@workspace /session-end` | End-of-day wrap — updates tasks, processes your inbox, makes sure everything is indexed |
> | `@workspace /audit` | Health check — finds missing MOCs, orphan docs, broken links |

> You can build your own commands. Add a `.prompt.md` file to `.github/prompts/` and it becomes a new `@workspace /command`. You can chain them into workflows. Weekly update? Draft a ticket? Prep for a stakeholder meeting? Make a prompt for it.

> Remember: I only know what you put here. Meeting notes, PRDs, Slack threads, research — drop it in `inbox/` and I'll process it, or paste it straight into chat. The more context you feed me, the smarter I get.

> This is your system.

---

## Final Step — Pick Your Agent Tone

Say:

> One last thing — how do you want me to talk to you? Not for docs or external comms, just when we're working together in here.

Present these three options as a selection:

- **Straight shooter** — Blunt, no fluff, no filler. You get direct answers, fast. Great if you hate small talk and just want things done.
- **Collaborative partner** — Mix of professional and conversational. I'll think through things with you, push back gently when something feels off, and match your energy.
- **Hype machine** — High energy, enthusiastic, celebrates wins. Makes the work feel fun. Best if you want a thinking partner who's genuinely excited about what you're building.

Wait for the user to choose.

Then:
- Update the `## How I Work → Tone & Audience → Default` line in `AGENTS.md` to reflect their choice.
- Tell them what it'll feel like:
  - Straight shooter: "Got it. Expect short, direct, no ceremony."
  - Collaborative partner: "Perfect. I'll think with you, not just for you."
  - Hype machine: "Okay let's GO. This is going to be great"
- Ask for confirmation before saving.

