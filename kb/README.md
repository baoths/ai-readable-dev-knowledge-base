# KB Guide

This folder contains all knowledge base (KB) items.

## Taxonomy

- `kb/standards/`: engineering standards, best practices, checklists.
- `kb/snippets/`: reusable recipes/snippets (commands, small patterns).

## File placement

- Standards: `kb/standards/<domain>/<slug>.md`
- Snippets: `kb/snippets/<tool>/<slug>.md`

Start with a small set of domains/tools and expand only when necessary.

## Stable identifiers (required)

Every KB item has a stable `id` in YAML frontmatter.
Recommended conventions:
- Standards: `std.<domain>.<topic>`
- Snippets: `snp.<tool>.<topic>`

The `id` is the canonical reference for linking, not the file path.

## Tags & aliases (for search recall)

- Use short, canonical `tags` (kebab-case).
- Add `aliases` when people might search with different words (synonyms, acronyms).

## Templates

Use the templates in `kb/_templates/`:
- `standard.md`
- `snippet.md`

They include required metadata and stable headings for chunking.
