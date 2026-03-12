---
description: "Disable automatic file creation — the agent will show proposed changes and ask for confirmation before writing"
---

# Disallow Automatic File Creation

1. Read `AGENTS.md` and find the line containing `<!-- file-creation-mode:`.
2. **If already set to `manual`:** say "Already disabled — I'll ask for confirmation before writing files."
3. **If set to `automatic`:** replace `<!-- file-creation-mode: automatic -->` with `<!-- file-creation-mode: manual -->`, then say:

> "Done. I'll now show proposed changes and ask for confirmation before creating or updating files. Run `/allow-automatic-files-creation` to switch back."
