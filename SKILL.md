---
description: "Write, edit, and version Product Requirements Documents with local iteration and intentional Notion syncing. Draft and edit locally as much as you want. Push to Notion when ready. Pull feedback daily at 8am. View markdown anytime in Claude."
---

# Weaver PRD Writer + Notion Sync

## Overview

This skill manages the complete PRD lifecycle with **local-first iteration** and **intentional Notion syncing** (like git). Work locally as much as you want. When ready, push to Notion for stakeholder review. Pull feedback automatically daily at 8am.

**Core commands:**
- **Draft a new PRD** — Create from scratch, guided or brain-dump (local only)
- **Edit the active PRD** — Revise and iterate locally (no Notion sync)
- **Push** — Sync current local version to Notion (creates Changelog entry)
- **Pull** — Fetch new feedback from Notion into your local Feedback Log
- **View** — Display any PRD's markdown directly in Claude
- **Check for feedback** — Manual check for Notion comments (or automatic daily at 8am)

## What you need

- **Notion connector** configured and authenticated in Cowork settings
- Access to the Notion PRD Repository database (data source ID: `8df71b3d-cc67-4d44-bb7a-87f096bdf14c`)
- **Daily 8am feedback check enabled** (optional, recommended)

## How to use

### 1. Draft a new PRD (local)

Ask Claude to draft a new PRD. You can:

**Option A — Guided workflow:** "Draft a new PRD for [feature/project name]"
Claude will prompt you through the PRD structure: goals, non-goals, scope, success metrics, implementation, and risks.

**Option B — Brain dump:** "Draft a PRD for [feature/project]. Here's what we're building: [paste your notes/spec/requirements]"
Claude will organize your text into PRD structure and ask clarifying questions.

**What happens:**
- Creates a local `.md` file: `prd-name-v0.1.md`
- Auto-displays the markdown for your review
- Becomes the "active PRD" for this session
- **NOT synced to Notion yet** — only local

---

### 2. Edit the active PRD (local, iterate freely)

Ask Claude: "Edit the PRD" or "Update the PRD with [your changes]"

Claude will:
1. Fetch your current local PRD (the active one)
2. Apply your changes
3. Auto-increment the version locally (v0.1 → v0.2 → v0.3, etc.)
4. Create new file: `prd-name-v0.2.md`
5. Auto-display the updated markdown for review
6. **NOT synced to Notion yet** — still local only

Iterate as much as you want in a day. Each edit increments the version locally. No Notion clutter.

---

### 3. Push to Notion (when ready to share)

Ask Claude: "Push" or "Push the PRD"

Claude will:
1. Take your current local version (e.g., v0.4 after multiple edits)
2. Sync it to your Notion PRD Repository
3. Create a Notion Changelog entry with the version, date, and auto-generated summary
4. Update the Notion page with your latest content and metadata
5. Confirm the push is complete

Now stakeholders see your latest version. Notion's Changelog stays clean—only pushed versions appear.

---

### 4. Pull feedback from Notion

**Manual pull:** Ask Claude "Pull" or "Pull feedback"

Claude will:
1. Fetch any new comments from your Notion PRD page
2. Add them to your local Feedback Log
3. Display the new feedback for your review

**Automatic daily pull:** Every day at 8:00am, Claude automatically:
1. Checks your active PRD for new Notion comments
2. Pulls any new feedback to your local Feedback Log
3. Notifies you if there's new feedback: "New feedback on [PRD name]—[count] comments"

You never miss stakeholder input.

---

### 5. View the active PRD (anytime)

Ask Claude: "Show me the PRD", "View", or "Display the markdown"

Claude will instantly fetch and display your current local markdown. No Notion call—instant view.

---

## Active PRD concept

The **active PRD** is whichever PRD you're currently working on in the conversation.

- After you draft or edit a PRD, it becomes active
- Commands like "Edit", "Push", "Pull", and "View" operate on the active PRD
- To switch: "Switch to [different PRD name]" or "Edit the [other PRD name]"

---

## Workflow example

```
Draft a new PRD for AI Benchmarking Tool
→ Creates prd-ai-benchmarking-v0.1.md (local)
→ Displays markdown
→ Becomes active PRD

Edit the PRD. Add success metrics.
→ Updates to prd-ai-benchmarking-v0.2.md (local)
→ Displays updated v0.2
→ Still local only

Edit the PRD. Clarify scope.
→ Updates to prd-ai-benchmarking-v0.3.md (local)
→ Displays updated v0.3

Push
→ Syncs v0.3 to Notion
→ Creates Changelog entry in Notion
→ Stakeholders see v0.3

[Next day, stakeholders comment in Notion...]

8:00am automated check
→ Pulls 3 new comments from Notion
→ Adds to local Feedback Log
→ Notifies: "New feedback on AI Benchmarking Tool—3 comments"

Pull
→ (or let the auto-check do it)
→ Display your Feedback Log

Edit the PRD. Address feedback.
→ Updates to prd-ai-benchmarking-v0.4.md (local)
→ Displays updated v0.4

Push
→ Syncs v0.4 to Notion
→ Changelog now shows v0.3 and v0.4
```

---

## File naming & versioning

Each PRD has distinct files per version:
- `prd-name-v0.1.md`, `prd-name-v0.2.md`, `prd-name-v0.3.md`, etc.
- All files are stored locally
- View always shows the latest version
- Notion Changelog shows all pushed versions

---

## Tips & best practices

- **Work locally first** — Draft and edit as much as you want before pushing. No Notion updates until you push.
- **Push when confident** — Each push creates a Notion Changelog entry. Push when the version is ready for stakeholder review.
- **Pull feedback daily** — Let the 8am automatic check keep you informed, or pull manually anytime.
- **Active PRD simplifies commands** — After drafting, just say "Edit", "Push", or "View" without repeating the PRD name.
- **Notion is source of truth for stakeholders** — Your local markdown is your working copy. Notion is where stakeholders leave feedback.
- **Two-way sync** — Push your work to Notion, pull their feedback back. Both directions keep you aligned.

---

## What Claude does

1. **Infer intent** — Detect draft / edit / push / pull / view from your request
2. **Track active PRD** — Remember which PRD you're working on in the conversation
3. **Manage files locally** — Create, update, and retrieve markdown files with version tracking
4. **Version auto-increment** — On each edit, bump the version and create a new file
5. **Generate content** — Draft or refine the PRD body based on your input
6. **Notion sync (on push)** — Send current version to Notion, create Changelog entry, update stakeholder-facing page
7. **Pull feedback** — Fetch Notion comments and log them in your local Feedback Log
8. **Auto-display** — After draft/edit, automatically show you the updated markdown for review
9. **Daily feedback check** — Every day at 8am, check for new Notion comments and notify you
