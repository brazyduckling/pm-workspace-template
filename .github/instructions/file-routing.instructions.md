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
| Decision | `docs/<project>/decisions/` |
| PRD or spec | `docs/<project>/prds/` |
| Cross-project / org context | `docs/general/` |
| Task | `ops/tasks.md` (append) |
| Reminder | `ops/reminders.md` (append) |
| Raw unprocessed input | `inbox/` |
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
    ├── decisions/
    └── prds/

ops/
├── tasks.md
└── reminders.md

inbox/
```

Directories are created on first use.

## Naming Conventions

| Type | Pattern | Example |
|---|---|---|
| Meeting notes | `YYYY-MM-DD-topic-slug.md` | `2026-03-04-kickoff-sync.md` |
| PRDs, decisions, other | `descriptive-slug.md` | `payment-flow-prd.md` |

## New Project Creation

1. Check if content fits an existing MOC scope
2. If not, create `docs/<project-name>/` + `<project-name>-moc.md`
3. Add it to `docs/index.md`
4. Add it to the Knowledge Graph in `AGENTS.md`

## MOCs

Every `docs/` subfolder has a `<folder>-moc.md` navigational index.

- List every doc with `[[wikilink]]` + short description
- Add new files to the relevant MOC when created
- Keep MOCs updated as files change
