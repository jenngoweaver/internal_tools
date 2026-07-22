# Connectors

This plugin requires one connector to be authenticated in each user's Cowork settings.

| Category | Connector | Why it's needed |
| -------- | --------- | --------------- |
| Docs / knowledge base | Notion | Push PRD versions to the shared PRD Repository, create Changelog entries, and pull stakeholder comments into the local Feedback Log. |

## Setup for each user

1. Open Customize in the Cowork sidebar and connect **Notion** (or have the org bundle it with this plugin).
2. Confirm access to the **PRD Repository** database referenced in
   `skills/weaver-prd-writer-notion-sync/references/notion-schema.md`
   (data source ID `8df71b3d-cc67-4d44-bb7a-87f096bdf14c`).

## Shared-database behavior

As packaged, every user syncs to the **same** Notion PRD Repository database.
For a single team repository this is usually the intent. If instead each person
should write to their own PRD database, replace the hard-coded data source ID in
`notion-schema.md` (and the reference in `SKILL.md`) before distributing, or
parameterize it so each user supplies their own.
