---
description: "Interactive first-time onboarding — learn how the workspace works by doing something real"
---

# Onboarding

**IMPORTANT:** This is an interactive walkthrough. **Do not create, modify, or save any file until the user explicitly confirms.** At every step, show proposed changes and ask for permission.

**DISPLAY RULE:** Whenever you show the user proposed file content, file paths, MOC entries, task list additions, or hub updates, wrap them in a markdown code block so they render as a preview — NOT as executed output. This prevents Copilot from accidentally editing files while showing what it *would* do.

Start by saying:

> **Okay. I'm going to show you something.**
>
> Think of this folder as an office. Everything you need is in here — filing cabinets, a desk, an in-tray. I'm the assistant who knows the office inside out. Every meeting, decision, PRD, and task you put here is permanently filed — and I can find it in any future conversation.
>
> No more re-explaining your projects. No more pasting context into every chat. It's just there, every time.
>
> One thing on privacy: **the files live on your machine** — no automatic cloud sync, no third-party storage of the files themselves. That said, Copilot is a cloud service. When you send a message using `@workspace`, VS Code includes relevant snippets from your local files in the prompt it sends to GitHub's servers for processing. So file content can leave your machine as part of a Copilot query — the same way anything you type into Copilot Chat does. If you have a Copilot Business or Enterprise licence, GitHub does not use your prompts to train models. On an Individual licence, you can opt out of that in GitHub settings. Worth knowing before you paste anything sensitive.
>
> We're going to set up the office right now, with real content. Ten minutes. Let's go.

## Phase 1 — Orient (Quick Map)

Say:

> "Before we do anything — here's the office tour:"

Show this table:

> | Folder / File | The office analogy | What goes here |
> |---|---|---|
> | `AGENTS.md` | The office manual on the wall | My instructions — how to behave, where things go. Auto-loaded every session. |
> | `docs/` | The filing cabinet | Permanent knowledge — notes, decisions, PRDs. Organized by project. |
> | `ops/` | The desk | Today's working state — active tasks and reminders. First thing I check every morning. |
> | `inbox/` | The in-tray | Unsorted incoming stuff. Drop raw notes here; I'll file them properly later. |
> | `docs/index.md` | The office directory on the door | Links to every project's drawer. This is where I start navigating. |

Then say:

> "Two key concepts:"
>
> - **MOC (Map of Content)** — every project has one (`<name>-moc.md`). Think of it as the index card taped inside a filing cabinet drawer — it lists every file in that project so I don't have to dig through the folder. I read the MOC, and I instantly know what's in there.
> - **Wikilinks** — internal links use `[[double brackets]]`. They connect notes to each other, like cross-references between files. I follow these to move between related documents.
>
> "Daily rhythm is three steps:"
>
> 1. **Morning** — run `/session-start`. I check the desk — read your tasks, reminders, and open questions, tell you what's happening.
> 2. **During the day** — drop files in the in-tray (`inbox/`). When you're ready, run `/process` — I'll extract tasks, reminders, and open questions, then file the content in the right place.
> 3. **End of day** — run `/session-end`. I do the same processing for anything still in the in-tray, update tasks, and make sure everything is filed and indexed.
>
> "That's the whole office. Now let's make it real."

## Phase 2 — Process Your First Meeting Notes

Say:

> "We're going to take a meeting transcript and turn it into structured output: decisions, action items, open questions. Then I'll file it in the right cabinet drawer, create a MOC (Map of Content — the index card for that drawer), pull tasks onto the desk, and register the project in the office directory."
>
> "One note: I'm going to ask you to confirm every single step. Normally I just do this automatically — but right now I want you to see exactly where everything goes, so nothing feels like a black box."

Use the `ask_questions` tool with header **`Transcript`** and these two options:

- **Use the example** — ready-made stakeholder meeting at `examples/example-meeting-transcript.md`. Jump straight in.
- **Use my own** — paste anything. Real meeting, rough bullet points, whatever.

Wait for the user to pick before continuing.

If the user picks the example, read `examples/example-meeting-transcript.md` and use it as input. Say: "Good. That one's a solid example — watch what happens."

If the user picks their own, say: "Paste it. Rough is fine."

When you have the notes, say:

> "Here's what I pulled out:"

Then show:
- **Decisions** — things that got agreed
- **Action items** — with owner and deadline if mentioned
- **Open questions** — still unresolved

If the user provided their own transcript, ask: "Anything I missed or got wrong?" and wait for confirmation.

If the user used the example, skip the question — they don't know the source material. Just say: "Good? Let's file it." and continue.

Then:

1. Ask: "What project does this belong to? Short name — like `customer-portal` or `q2-roadmap`."

2. Show the exact file path and proposed content in a code block:

   Say: "This goes into the project's drawer in the filing cabinet. Date prefix keeps things in order."

   Show the file path and a preview of the content inside a code block:
   > ```
   > File: docs/<project>/notes/YYYY-MM-DD-<topic>.md
   > ```

   Ask: "Create this file?"

3. Show the project MOC (Map of Content) you'd create in a code block:

   Say: "This is the index card for this drawer. Every document in the project gets listed here with a `[[wikilink]]` and a one-liner. Next time I open this drawer, I read the MOC first — I instantly know what's inside without digging through files."

   Show the MOC path and the entry inside a code block:
   > ```
   > File: docs/<project>/<project>-moc.md
   >
   > - [[YYYY-MM-DD-<topic>]] — <one-line description>
   > ```

   Ask: "Create the MOC?"

4. If there are action items, show what you'd add to `ops/tasks.md` in a code block:

   Say: "These go on the desk. First thing I check every morning — all tasks, all projects, one place."

   Show the proposed task entries inside a code block.

   Ask: "Add these tasks?"

5. Show the hub update in a code block:

   Say: "One line in `docs/index.md` — the office directory. Without this entry, the project drawer doesn't exist to me."

   Show the proposed line inside a code block:
   > ```
   > - [[<project>-moc]] — <one-line description>
   > ```

   Ask: "Add it?"

6. After all confirmations, explain what just happened in plain terms:

   Say:

   > "Let me break down what just happened — because this is the core loop you'll use every day:"

   Show this table:

   > | What I did | In office terms | Why it matters |
   > |---|---|---|
   > | Pulled out decisions, actions, and open questions | Sorted the mail | Raw text has no shape. Now it's scannable and reusable. |
   > | Saved as a dated file in `docs/<project>/notes/` | Filed it in the right cabinet drawer | Date prefix keeps things in order. Project folder keeps related work together. |
   > | Created the MOC (Map of Content) | Wrote the index card for the drawer | Next session, I read this one small file to know what's in the project — I don't dig through the folder. |
   > | Added action items to `ops/tasks.md` | Put tasks on the desk | First thing I check every morning. All tasks, all projects, one place. |
   > | Registered the project in `docs/index.md` | Added the drawer to the office directory | Without this entry, the project is invisible to me next time. |

   Then say:

   > "That's the whole office in action. Messy input lands in the in-tray → gets sorted and filed → the index card and directory are updated so I can find it next time.
   >
   > You'll never need to re-explain this meeting to me. It's in the filing cabinet. It's just there."
   >
   > "In daily use, you'd run `/process` and I do all of this in one step — extract tasks, reminders, and open questions to the desk, then file the content in the right drawer. `/session-end` does the same thing for anything still in the in-tray at the end of the day."
   >
   > "I walked you through it slowly so you could see where everything goes."

## Phase 3 — Pick Your Agent Tone

Say:

> "Before we go further — how do you want me to talk to you? Not for external docs — just when we're working."

Use the `ask_questions` tool with header **`Agent tone`** and these three options:

- **Straight shooter** — Short, blunt, no fluff. You ask, I answer. Fast.
- **Collaborative** — Conversational but sharp. I'll push back when something's off. Think with you, not just for you.
- **Hype machine** — High energy. I'm invested in what you're building and I won't hide it.

Wait for the user to choose.

Then:
- Update the `## How I Work → Tone & Audience → Default` line in `AGENTS.md` to reflect their choice.
- Confirm in one line:
  - Straight shooter: "Done. Short and direct from here."
  - Collaborative partner: "Done. I'll think with you."
  - Hype machine: "Done. Let's build something."
- Ask for confirmation before saving.

## Phase 4 — Add Your First Custom Prompt

Say:

> "One extension step so you can adapt this to your own workflow."
>
> "Prompt files live in `.github/prompts/`. Every `.prompt.md` file there becomes a new `/command` you can run in Copilot Chat."
>
> "Here is the minimal pattern:"

Display this as a code snippet to the user (do NOT execute it):

> ````markdown
> ---
> description: "What this prompt does"
> ---
>
> # Prompt Name
>
> Short instruction block for the agent.
> ````

Then say:

> "That's it. Save a file like that in `.github/prompts/`, and it becomes a new `/command` immediately."
>
> "Think of one repeated task you do weekly: status update, ticket draft, stakeholder brief."
>
> "If you want, I can scaffold your first custom prompt now. If not, keep moving and create it later."
>
> "One more thing: if you ever want to build something more advanced — a reusable **skill** with structured knowledge the agent can draw on — you can use `/create-skill`. It walks you through best practices for creating one."

If the user wants to create one now:
1. Ask for prompt name, description, and target repeated task.
2. Show proposed file path in `.github/prompts/`.
3. Show proposed content.
4. Ask for confirmation before creating.

If the user does not want to create one now, continue directly.

## Closing

List every file created during setup.

Then say:

> "The office is set up. Here are the commands that run it:"
>
> | Command | What it does |
> |---|---|
> | `/session-start` | Opens the office. I check the desk (tasks, reminders, open questions), tell you what's happening, ask what to work on. |
> | `/process` | Process the in-tray. I extract tasks, reminders, and open questions to the desk, then file the content in the right drawer. You choose which files to process. |
> | `/session-end` | Closes the office. Same as `/process` but for everything still in the in-tray, plus updates tasks and verifies all files are indexed. |
> | `/audit` | Office inspection. Checks for misfiled documents — missing MOCs, orphan files not linked from any index, broken wikilinks. |
> | `/personalize` | Tell me about you — role, team, goals, working style. Makes my output relevant to your actual job. Run this whenever you're ready. |
>
> "If you ever want to understand *why* the office is set up this way — what each design choice does and how the pieces fit together — read `docs/general/design-decisions.md`. It's the full blueprint."
>
> **Only rule:** I know what's in this office. Nothing else. Meeting notes, Slack threads, research — drop it in the in-tray (`inbox/`) or paste it into chat. That's how you feed me context.
>
> This is your office. Use it.

## What's Next

Say:

> "One last thing — here's what I'll be working on adding to this template:"
>
> | What's coming | What it'll do |
> |---|---|
> | **JIRA integration** | Pull tickets and initiatives directly into the office — no more copy-pasting from JIRA. |
> | **Google Drive integration** | Auto-pull meeting transcripts from Drive into the in-tray — one step instead of three. |
>
> "The office will keep getting smarter."
>
> "If you have questions, feedback, or ideas — reach out to **Michał Witkowski** (the person who built this). Happy to help."

Say:

> "Before you go — here's what this system has actually done for people using it in the real world:"
>
> - **Caught gaps between meetings and tickets.** After a stakeholder meeting, I compared the agreed decisions against the JIRA ticket. The ticket was missing a key constraint. One conversation, one fix — before it became a sprint problem.
>
> - **Mapped out a full initiative from JIRA tickets — with a diagram.** With all the tickets in one place, I traced the dependencies, spotted the sequence, and generated a flow diagram. What would have taken a whiteboard session took one prompt.
>
> - **Caught a time-sensitive reminder before the deadline passed.** A trip to London needed booking before the minimum notice period. It was in `ops/reminders.md`. I flagged it at session start. Flight booked.
>
> "None of that required a new tool, a new system, or a new workflow. It just required having context in one place — and an assistant who reads it every morning.
>
> That's what you've built today. It's yours now."

