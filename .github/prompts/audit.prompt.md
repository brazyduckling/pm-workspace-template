---
description: "Audit workspace structure — MOC coverage, orphans, dead links, and index sync"
---

**DO NOT auto-fix anything. Present findings first, then ask for confirmation before making changes.**

## Checks

### 1) MOC Coverage
- List top-level folders in `docs/`
- Verify each has `<folder>-moc.md`
- Report missing MOCs

### 2) Orphan Documents
- Scan markdown files in `docs/` (excluding MOCs)
- Verify each appears as a `[[wikilink]]` in at least one MOC
- Report unindexed docs

### 3) Dead Links in MOCs
- Read each MOC and validate `[[wikilink]]` targets exist
- Report broken links

### 4) Knowledge Graph Sync
- Compare AGENTS.md Knowledge Graph entries against actual MOC files
- Report entries that are missing/stale in either direction

### 5) Hub Sync
- Verify `docs/index.md` includes all project MOCs
- Verify `docs/index.md` lists all ops/ files (`tasks`, `reminders`, `open-questions`)
- Report missing hub links

### 6) Frontmatter Completeness
- Check docs in `docs/` for required fields:
  - title
  - description
  - date
  - status
  - topics
- Report missing/empty fields

### 7) Archive Integrity
- Check docs in `docs/` with a `source` frontmatter field: verify the referenced archive file exists
- Check every `archive/<project>/` folder has a `<project>-archive-moc.md`
- Check `archive/archive-index.md` lists all project folders in `archive/`
- Report missing archive files, missing archive MOCs, and unlisted project folders

## Output

Provide results grouped by category and include clear file paths for each issue.

After reporting, ask:
"Want me to fix these issues?"

Only apply fixes explicitly confirmed by the user.
