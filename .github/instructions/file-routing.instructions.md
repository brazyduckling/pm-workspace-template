---
name: File Routing
description: Where to create and find documents — routing rules and folder structure
applyTo: "docs/**"
---

# File Routing

## Routing Rules

| Content type | Destination |
|---|---|
| Meeting notes | `docs/<project>/meeting-notes/` |
| PRD or spec | `docs/<project>/prds/` |
| Cross-project / org context | `docs/general/` |
| Task | `ops/tasks.md` (append) |
| Reminder | `ops/reminders.md` (append) |
| Open question | `ops/open-questions.md` (append) |
| Raw unprocessed input | `inbox/` |
| Raw original (after processing) | `archive/<project>/` |
| MOC (index) | `docs/<folder>/<folder>-moc.md` |

## Folder Structure

```
docs/
├── index.md
├── general/
│   ├── general-moc.md
│   ├── personal-context.md
│   └── org-context.md
└── <project-name>/
    ├── <project-name>-moc.md
    ├── meeting-notes/
    └── prds/

ops/
├── tasks.md
├── reminders.md
└── open-questions.md

inbox/

archive/
├── archive-index.md
└── <project-name>/
    └── <project-name>-archive-moc.md
```

Directories are created on first use.

## Naming Conventions

| Type | Pattern | Example |
|---|---|---|
| Meeting notes | `YYYY-MM-DD-topic-slug.md` | `2026-03-04-kickoff-sync.md` |
| PRDs, other | `descriptive-slug.md` | `payment-flow-prd.md` |

## New Project Creation

1. Check if content fits an existing MOC scope
2. If not, create `docs/<project-name>/` + `<project-name>-moc.md`
3. Add it to `docs/index.md`

## MOCs

Every `docs/` subfolder has a `<folder>-moc.md` navigational index.

- List every doc with `[[wikilink]]` + short description
- Add new files to the relevant MOC when created
- Keep MOCs updated as files change

## Archive Routing

After processing an inbox file to its permanent `docs/` location:

1. **Never delete the original from `inbox/`.** Archive it instead.
2. Rename to a descriptive title with date prefix (e.g., `2026-03-12-raw-kickoff-transcript.md`)
3. Move to `archive/<project>/`
4. If this is the first file in `archive/<project>/`: create `<project>-archive-moc.md` and add it to `archive/archive-index.md`
5. Add a `[[wikilink]]` entry to the project's archive MOC
6. Add `source: "[[archived-filename]]"` to the processed note's frontmatter
