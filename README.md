# AI-Readable Developer Knowledge Base

A structured, bilingual (VI/EN) knowledge base for engineering standards and reusable snippets.
Designed to be:
- Easy to browse and search (GitHub search-friendly)
- Easy to reuse (copy-pasteable recipes/snippets)
- Easy to parse and chunk for future vectorization/RAG (stable metadata + headings)

---

## What lives here

- **Standards**: engineering guidelines, checklists, conventions, best practices.
- **Snippets**: small, reusable “recipes” (commands, patterns, templates).

---

## Repo structure

```
kb/
  standards/
  snippets/
  _templates/
```

- KB items are Markdown files under `kb/`.
- **One topic per file**. Keep items short and self-contained.

---

## KB item format (AI- & human-friendly)

Every KB item:
1. Starts with **YAML frontmatter** metadata (machine-readable)
2. Contains two sections: **Vietnamese** and **English**
3. Uses stable headings for consistent chunking:
   - TL;DR
   - Context/Why
   - Guidance
   - Examples
   - Pitfalls
   - References

---

## How to add a new KB item

1. Copy a template from `kb/_templates/`
2. Pick an `id` that is unique and stable
3. Fill in `tags` and (optional) `aliases` for better search recall
4. Write Vietnamese + English sections (keep them equivalent)

See `CONTRIBUTING.md` for the full checklist.

---

## Contributing

Contributions are welcome.

- Start here: [CONTRIBUTING.md](CONTRIBUTING.md)
- Please follow the [Code of Conduct](CODE_OF_CONDUCT.md)

When you submit a PR, you confirm you have the right to contribute the content and that
it can be licensed under this project’s license.

---

## Search tips

Within GitHub, search by:
- `id:` (stable identifier)
- `tags:` (topic/tool/language)
- `aliases:` (synonyms)

Example queries:
- `id:std.code-review` 
- `tags:security tags:owasp`
- `aliases:lint`

---

## License

This project is licensed under the MIT License.

See [LICENSE](LICENSE).

---

## Security

If you discover a security issue, please follow [SECURITY.md](SECURITY.md).

---

## Support

See [SUPPORT.md](SUPPORT.md).
