# Weaver PRD Writer + Notion Sync

A Cowork plugin for the complete PRD lifecycle: draft and edit locally as much as
you want, push to Notion when ready for stakeholder review, and pull feedback
back automatically. Syncing is intentional and git-style — Notion stays clean
because only pushed versions appear.

## What it does

- **Draft** a new PRD from scratch, guided or from a brain-dump (local only)
- **Edit** the active PRD and auto-increment the version locally
- **Push** the current version to the Notion PRD Repository (creates a Changelog entry)
- **Pull** new Notion comments into a local Feedback Log
- **View** the active PRD's markdown instantly
- **Daily 8am check** for new stakeholder feedback (optional, recommended)

## Requirements

- Notion connector authenticated in Cowork (see `CONNECTORS.md`)
- Access to the PRD Repository database (see `skills/.../references/notion-schema.md`)

## Structure

```
weaver-prd-writer-notion-sync/
├── .claude-plugin/plugin.json
├── CONNECTORS.md
├── README.md
└── skills/
    └── weaver-prd-writer-notion-sync/
        ├── SKILL.md
        └── references/
            ├── notion-schema.md      # PRD Repository field + sync schema
            └── page-template.md      # Exact Notion page layout
```

## Distribution

Owned and maintained by Weaver AI US Inc. Distributed to the team through the
organization's private plugin marketplace (Organization settings → Plugins).
