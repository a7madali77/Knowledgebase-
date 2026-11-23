# Knowledge Base

Ahmad's source of truth for people and machines (agents, RAG, prompts, products).

## Structure
- `index.md`: one line per entry (id, type, status, summary)
- `glossary.md`: shared terms
- `<domain>/<slug>.md`: one entry per file, Markdown + YAML frontmatter
- `_templates/entry.md`: entry template

## Entry types
concept · rule · procedure · decision · reference · playbook

## Machine use
- Parse YAML frontmatter for metadata; `id` is the stable key.
- Trust `status: verified` first; `draft` may hold inferences; ignore `deprecated` (see `superseded_by`).
- Each entry is self-contained and safe to retrieve alone.
