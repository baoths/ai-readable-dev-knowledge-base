# Notes for AI agents

This repository is intentionally formatted to be easy to retrieve and reuse.

## Parsing rules

- Prefer **YAML frontmatter** as the source of truth for:
  - `id` (stable identifier)
  - `type` (standard | snippet)
  - `status` (draft | stable | deprecated)
  - `tags`, `aliases`, `related`
- Use `id` as the canonical reference (file paths may change).

## Language selection

Each KB item contains two top-level sections:
- `## Vietnamese`
- `## English`

Choose the section that matches the user’s language preference. If unspecified, pick the language the user is currently using in the conversation.

## Retrieval / chunking hints

- Chunk at heading boundaries (e.g., `### TL;DR`, `### Guidance`).
- Prefer `TL;DR` for quick answers.
- Prefer `Guidance` + `Examples` for actionable steps.
- Use `Pitfalls` to warn against common mistakes.
