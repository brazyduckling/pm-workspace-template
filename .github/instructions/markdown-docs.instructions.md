---
name: Document Conventions
description: Frontmatter and formatting rules for docs
applyTo: "docs/**/*.md"
---

# Document Conventions

> Applies to files in `docs/` only.

## YAML Frontmatter

Every document must include:

```yaml
---
title: Document Title
description: "One sentence that adds info beyond the title."
date: DD MMM YYYY
status: draft | in-review | approved | archived
topics: [parent-moc-name]
---
```

### Field Rules

- `title`: clear and human-readable
- `description`: must differ from title
- `date`: format `DD MMM YYYY`
- `status`: one of `draft`, `in-review`, `approved`, `archived`
- `topics`: MOC membership list (plain text names)
- `source` *(optional)*: `"[[archived-filename]]"` — links to the raw original in `archive/`. Added automatically when a file is processed from `inbox/`.

## Internal Links

- Use `[[wikilinks]]` for internal references
- Use `[[filename]]` or `[[filename#Section]]`
- No `.md` extension, no path
- Use standard markdown links for external URLs only

## Formatting

- Dates use `DD MMM YYYY`
- Unknown values use `TBD`
- Filenames use `kebab-case.md`
