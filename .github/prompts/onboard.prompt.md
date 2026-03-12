---
description: "Interactive first-time onboarding — see the workspace work on real content"
---

# Onboarding

**This prompt is the exception to the confirm-before-write rule. Process everything without asking first, then explain what you did in the recap.**

Start by saying:

> "Think of this folder as an office. Filing cabinets, a desk, an in-tray. I'm the assistant."
>
> Here's the layout:

Show this table:

> | Folder / File | What goes here |
> |---|---|
> | `AGENTS.md` | My instruction manual — how to behave, where things go. Auto-loaded every session. |
> | `docs/` | The filing cabinet — permanent knowledge, organized by project. |
> | `ops/` | The desk — tasks, reminders, and open questions. First thing I check every morning. |
> | `inbox/` | The in-tray — drop raw notes here, I'll file them properly. |
> | `archive/` | Storage room — raw originals after processing. Only pulled out when you need exact wording. |
> | `docs/index.md` | The office directory — links to every project. Where I start navigating. |

Say: "That's the layout. Now let's see it handle a real transcript."

Use the `ask_questions` tool with header **`Ready to see it in action?`** and a single option:

- **Let's go**

## Pain Point Hook

After the user clicks, say:

> "Here's the thing about using AI as a PM.
>
> Chat forgets everything. Gems and GPTs have static context — stale in a week.
>
> This is different. Your context grows every time you work. It connects things like your brain does.
>
> Let me show you."

## Demo — Process a Transcript

Say: "I need a meeting transcript to work with — pick one below."

Use the `ask_questions` tool with header **`Transcript`** and these two options:

- **Use the example** — ready-made meeting transcript at `examples/example-meeting-transcript.md`
- **Use my own** — I'll paste something

If the user picks the example: read `examples/example-meeting-transcript.md` and use it as input.

If the user picks their own: say "Paste it. Rough is fine." and wait.

When you have the transcript:

1. Auto-pick a project name from the content — do NOT ask the user. Infer it from the topic, people mentioned, or domain. Use a short slug like `customer-portal` or `driver-tracking`.

2. Process everything WITHOUT asking for confirmation:
   - Extract decisions, action items, and open questions
   - Create `docs/<project>/meeting-notes/YYYY-MM-DD-<topic>.md` with structured content and proper frontmatter
   - Create `docs/<project>/<project>-moc.md` linking to the note
   - Add action items to `ops/tasks.md`
   - Add the project to `docs/index.md`

3. Then show the recap as a punchy bullet list:

   > "Done. Here's what just happened:
   > - Pulled out decisions, tasks, and open questions — raw text turned into structure
   > - Filed the note in `docs/<project>/` — so I find it next time without you re-explaining
   > - Tasks went to `ops/tasks.md` — one list, all projects, checked every morning
   > - Project registered in `docs/index.md` — it's a map for me so I go straight there instead of looking at everything to find it
   > - In daily use, `/process` and `/session-end` also save originals in `archive/` — exact wording preserved when you need it. Great for pulling evidence during performance reviews ;)"

## Session-Start Preview

Say: "I can also preview your daily morning check-in — the `/session-start` flow."

Use the `ask_questions` tool with header **`Want to see what your morning looks like?`** and these two options:

- **Yes, show me**
- **Skip — I'll check later**

If yes: read `ops/tasks.md`, `ops/reminders.md`, and `ops/open-questions.md`. Summarise them exactly as `/session-start` would — what's on the desk, what's due, what's unresolved. Keep it brief, 5–10 lines. Then say: "That's `/session-start`. One command. Full picture of your day."

If skip: continue.

## Daily Rhythm

Say:

> "Three commands run the whole thing:"
>
> | Command | What it does |
> |---|---|
> | `/session-start` | I check tasks, reminders, open questions. Tell you what's on your plate. |
> | `/process` | I take what's in `inbox/`, extract tasks, file the content, archive the original. |
> | `/session-end` | Same as `/process` for everything still in the inbox, plus I verify indexing. |
> | `/audit` | I check for misfiled docs, broken links, missing indexes. |

## Goodbye

List every file created during this session.

Then say:

> "I create and update files automatically by default — no confirmation needed. If you'd prefer I ask first, run `/disallow-automatic-files-creation`. Re-enable anytime with `/allow-automatic-files-creation`.
>
> No more re-explaining context every chat. No more lost action items. No more forgotten decisions. It's all here now.
>
> Make this place your own. All the logic is in `docs/general/design-decisions.md`. Want me to act differently? Just tell me and say 'always do it from now on.' When you're ready, try `/create-skill` to build your own reusable skills.
>
> PS. You can personalize me a bit more by running `/personalize` ;)"

