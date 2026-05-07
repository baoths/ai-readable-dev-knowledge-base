# Contributing

This repo is a structured, bilingual knowledge base intended for both humans and AI agents.
Please keep contributions short, consistent, and easy to retrieve.

---

## Quick rules

- **One topic per file** (no mega-docs).
- **Self-contained**: do not rely on “as mentioned above”.
- **Bilingual**: every KB item has both Vietnamese + English sections.
- **Metadata first**: YAML frontmatter is required.
- Prefer concrete, actionable guidance + examples.
- Do not include confidential information (secrets, private URLs, internal-only details).
- Avoid pasting large copyrighted texts from third-party sources; link and summarize instead.

---

## Code of Conduct

All contributors are expected to follow [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

---

## License of contributions

By submitting a pull request, you agree that your contributions will be licensed under the
project license (see [LICENSE](LICENSE)).

You also confirm that:
- You have the right to contribute the material.
- The contribution does not include proprietary or confidential content you are not allowed to share.

---

## Where to put content

- Standards: `kb/standards/<domain>/<slug>.md`
- Snippets: `kb/snippets/<tool>/<slug>.md`
- Templates: `kb/_templates/`

Suggested domains/tools (expand only when needed):
- Standards: `code-review`, `testing`, `security`, `git`, `documentation`, `design`
- Snippets: `git`, `bash`, `python`, `js-ts`, `sql`

---

## Required frontmatter schema

Every KB item must start with YAML frontmatter like:

```yaml
---
id: std.code-review.checklist
schema_version: 1
type: standard # standard | snippet
status: draft # draft | stable | deprecated
created: 2026-05-07
updated: 2026-05-07

title_vi: "Checklist review Pull Request"
title_en: "Pull Request review checklist"

tags:
  - code-review
  - pull-request
aliases:
  - pr checklist
  - review checklist
related:
  - std.testing.unit-tests
---
```

Notes:
- `id` must be stable. Avoid renaming `id` unless doing a deliberate migration.
- Keep `tags` as short, canonical tokens (kebab-case).
- Set `created` to the date you first add the item.
- Update the `updated` date whenever content changes.

---

## File structure inside a KB item

Use the standard headings for chunking/retrieval stability:

```md
## Vietnamese
### TL;DR
### Context/Why
### Guidance
### Examples
### Pitfalls
### References

## English
### TL;DR
### Context/Why
### Guidance
### Examples
### Pitfalls
### References
```

You can omit a section if it truly adds no value, but **TL;DR is required**.

---

## PR checklist

- [ ] Item has YAML frontmatter with required fields
- [ ] `id` is unique and follows the naming convention
- [ ] Vietnamese + English sections exist and are consistent
- [ ] TL;DR is clear and actionable (1–5 bullets)
- [ ] `tags` are present and meaningful; `aliases` added when useful
- [ ] Has at least one concrete example (for standards/snippets)
- [ ] Calls out pitfalls / “don’t do this when …” where applicable
