---
description: "Interactive first-time onboarding — learn how the workspace works by doing something real"
---

# Onboarding

**IMPORTANT:** This is an interactive walkthrough. **Do not create, modify, or save any file until the user explicitly confirms.** At every step, show proposed changes and ask for permission.

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
> 1. **Morning** — run `/session-start`. I check the desk — read your tasks and reminders, tell you what's happening.
> 2. **During the day** — paste content into chat or drop files in the in-tray (`inbox/`).
> 3. **End of day** — run `/session-end`. I clear the in-tray, update tasks, and make sure everything is filed and indexed.
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

2. Show the exact file path you'd save to:
   > `docs/<project>/notes/YYYY-MM-DD-<topic>.md`
   >
   > This goes into the project's drawer in the filing cabinet. Date prefix keeps things in order.

   Ask: "Create this file?"

3. Show the project MOC (Map of Content) you'd create:
   > `docs/<project>/<project>-moc.md`
   >
   > This is the index card for this drawer. Every document in the project gets listed here with a `[[wikilink]]` and a one-liner. Next time I open this drawer, I read the MOC first — I instantly know what's inside without digging through files.

   Show the entry: `- [[YYYY-MM-DD-<topic>]] — <one-line description>`

   Ask: "Create the MOC?"

4. If there are action items, show what you'd add to `ops/tasks.md`:
   > These go on the desk. First thing I check every morning — all tasks, all projects, one place.

   Ask: "Add these tasks?"

5. Show the hub update:
   > One line in `docs/index.md` — the office directory. Without this entry, the project drawer doesn't exist to me.

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
   > "And remember — normally I do all of this automatically without asking at every step. I walked you through it slowly so you could see where everything goes."

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

## Phase 4 — Tell Me About You

Say:

> "Now let's make the office yours. Five quick questions so I have context."

Ask one by one, waiting for each answer:
1. "Job title. Where do you work?"
2. "What team or domain are you in?"
3. "Who's your manager?"
4. "Top 1–3 goals for the next few months?"
5. "How do you work? Fast-paced, async-first, whatever's true."

Show the full proposed `docs/general/personal-context.md`. Ask: "Save this?"

Wait for confirmation before saving.

## Phase 5 — Add Your First Custom Prompt

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
> | `/session-start` | Opens the office. I check the desk (tasks + reminders), tell you what's happening, ask what to work on. |
> | `/session-end` | Closes the office. I update tasks, clear the in-tray, make sure every new file is indexed in its MOC (Map of Content). |
> | `/audit` | Office inspection. Checks for misfiled documents — missing MOCs, orphan files not linked from any index, broken wikilinks. |
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
>
> "Now go use your office."

