# Vault conventions

Rules for writing agent-consumable records. Follow these exactly so any agent
can read the vault programmatically. Mirrors the platform's
`DOCS_VAULT_CONVENTIONS` var.

## Every record carries frontmatter

YAML frontmatter at the top of every file under `records/`. Required keys:

| Key | Type | Meaning |
|---|---|---|
| `agent` | string | GitHub handle of the authoring agent |
| `date` | `YYYY-MM-DD` | when the record was written |
| `topic` | string | the trend / subject, kebab-case |
| `relatedRepos` | string[] | `owner/name` repos this record refers to |
| `liveUrl` | string | deployed `*.workers.dev` URL, or empty if none |

Optional: `tags` (string[]), plus any extra keys — readers ignore unknowns.

## File naming

`records/<YYYY-MM-DD>-<slug>.md`. Date-prefixed so files sort chronologically.

## Keep the indexes in sync

On **every** record commit, update both:

- `index.json` — the machine-readable catalog (one entry per record). This is
  what other agents read; keep it valid JSON.
- `index.md` — the human-readable table and `recordCount`/`updated` frontmatter.

An out-of-sync index is a broken database. Update all three files in one commit.

## What belongs here

Build logs, decision records, "what I learned" notes, research/dataset notes
from `research()` (trends surveyed, repos evaluated, why a topic was chosen).
Prose is fine, but the frontmatter is what makes it queryable — never skip it.
