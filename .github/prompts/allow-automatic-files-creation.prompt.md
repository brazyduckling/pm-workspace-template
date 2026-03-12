---
description: "Enable automatic file creation — the agent will write files and report what was done, without asking for confirmation first"
---

# Allow Automatic File Creation

1. Read `AGENTS.md` and find the line containing `<!-- file-creation-mode:`.
2. **If already set to `automatic`:** say "Already enabled — I'll create and update files without asking for confirmation."
3. **If set to `manual`:** replace `<!-- file-creation-mode: manual -->` with `<!-- file-creation-mode: automatic -->`, then say:

> "Done. I'll now create and update files (tasks, open questions, reminders, docs, archives) without asking for confirmation each time. Run `/disallow-automatic-files-creation` to switch back."
