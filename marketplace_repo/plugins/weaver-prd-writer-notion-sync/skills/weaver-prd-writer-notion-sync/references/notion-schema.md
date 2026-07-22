# Notion PRD Repository Schema

## Database Overview

**Location:** https://app.notion.com/p/ebf913e7983e49f6be1940ad9eab8821  
**Data Source ID (for syncing):** `8df71b3d-cc67-4d44-bb7a-87f096bdf14c`  
**Filed under:** Product Requirements > Engineering & Product

---

## Field Definitions

### Name (Title)
- **Type:** Title
- **Required:** Yes
- **Purpose:** Unique identifier for the PRD. Used to match draft → edit → version bump operations.
- **Rules:** Must be unique within the database. Do not rename mid-lifecycle; rename in Notion first if needed.
- **Example:** "AI Agent Benchmarking Tool", "Revenue Cycle Automation Phase 2"

### Status (Select)
- **Type:** Select
- **Required:** Yes
- **Default for new PRDs:** Draft
- **Options:**
  - **Draft** — Initial creation, under active development, awaiting review
  - **In Review** — Submitted for stakeholder review, feedback phase active
  - **Approved** — Final sign-off received, ready for implementation. *When a PRD transitions from v0.x to Approved, Version auto-bumps to v1.0 as part of the same edit.*
  - **Superseded** — Replaced by a newer PRD; requires explicit reason entry in Changelog
  - **Rejected/Withdrawn** — Decision not to pursue; requires explicit reason entry in Changelog
- **Transitions:** Status changes to Superseded or Rejected/Withdrawn must be explicit and logged with a reason in a new Changelog row before the Status is changed.

### Version (Text)
- **Type:** Text
- **Required:** Yes
- **Default for new PRDs:** v0.1
- **Auto-increment rules:**
  - Edits increment within v0.x series: v0.1 → v0.2 → v0.3 (content changes)
  - Approval increments to v1.0: v0.x → v1.0 (only when Status changes to Approved and Version is still v0.x)
  - Post-v1.0, continue normal incrementing: v1.0 → v1.1 → v1.2
- **Track in Changelog:** Every version change gets a new Changelog row
- **Immutable:** Once a version is logged, it is never edited; only new versions are added

### Owner (Person)
- **Type:** Person
- **Required:** Yes
- **Set to:** Current Cowork user (auto-populated during draft)
- **Meaning:** Primary author/owner of the PRD. Can be updated if responsibility transfers.

### Category (Select)
- **Type:** Select
- **Required:** Yes
- **Options:**
  - Internal Tools
  - Client Delivery
  - Platform
  - Process
- **Set during:** Initial draft; can be changed via edit
- **Meaning:** Operational categorization for filtering and navigation

### Last Updated (Auto)
- **Type:** Auto — Last edited time
- **Read-only:** System-managed
- **Synced:** Updated whenever the PRD page is modified

### Created (Auto)
- **Type:** Auto — Created time
- **Read-only:** System-managed
- **Set:** On initial Notion page creation

---

## Relation to Page Content

The Notion page itself contains three structural sections:

1. **Header (compact, no duplication)**
   - Category and positioning summary
   - Contributors / stakeholders
   - Scope qualifiers that don't repeat the Status/Version/Owner/Category properties
   - Example: "Internal tool for engineering teams. Stakeholders: Product, Design, Eng."

2. **## Changelog (table, never edited)**
   - Columns: Version | Date | Changes
   - New rows always added to the top (newest first)
   - Rows are never edited or deleted, only appended
   - Every version change → new row
   - Example row: `v0.2 | 2026-07-10 | Added throughput/latency success metrics; clarified internal-only scope`

3. **## Feedback Log (table, appended as comments arrive)**
   - Columns: Date | Reviewer | Version Reviewed | Feedback | Status
   - Status options: Open / Addressed
   - Rows never deleted; closed feedback marked "Addressed" instead
   - Automatically populated from Notion comments via sync process
   - Example row: `2026-07-10 | Sarah Chen | v0.2 | Clarify data retention policy for benchmarks | Open`

4. **PRD body** — Standard sections: Goals, Non-Goals, Success Metrics, Scope, Implementation, Risks, Appendix, etc.

---

## Sync Behavior

### On Draft (new PRD)
- Create Notion page with Name, Status (Draft), Version (v0.1), Owner (current user), Category (user-specified)
- Populate page content with Header, empty Changelog (first row: "v0.1 | YYYY-MM-DD | Initial draft"), empty Feedback Log, and PRD body
- Create corresponding `.md` file locally

### On Edit (existing PRD)
- Fetch Notion page by Name search
- Auto-increment Version (v0.1 → v0.2)
- Generate Changelog row: `v0.2 | YYYY-MM-DD | [auto-generated change summary from user's edits]`
- Fetch any new Notion comments and add to Feedback Log (Status = Open)
- Update Notion page content and Version field
- Update `.md` file

### On Bump Version
- Fetch Notion page by Name search
- Auto-increment Version
- Generate Changelog row with user context (e.g., "Engineering sign-off")
- Fetch any new Notion comments and add to Feedback Log (Status = Open), reply confirming logged
- Update Version field in Notion
- Update `.md` file

### On Status transition (Approved / Superseded / Rejected-Withdrawn)
- Require explicit reason from user
- If Status → Approved and Version is v0.x, also auto-bump Version to v1.0
- Log reason in Changelog row before changing Status
- Update Status field in Notion

---

## Common Workflows

| Scenario | Action | Version Change | Status Change | Changelog Entry |
|----------|--------|-----------------|---------------|-----------------|
| Create new PRD | Draft | None (v0.1) | None (Draft) | "Initial draft" |
| Add features after feedback | Edit | v0.1 → v0.2 | None | "Added feature X; updated scope" |
| Incorporate legal review | Edit | v0.2 → v0.3 | None | "Incorporated legal review feedback" |
| Ready for implementation | Status change | None | Draft → Approved | "Approved for implementation"; auto-bump v0.3 → v1.0 |
| Replaced by newer spec | Status change | None | Any → Superseded | Reason: "Replaced by PRD-v2 with expanded scope" |
| Project cancelled | Status change | None | Any → Rejected | Reason: "Project deprioritized Q3 roadmap shift" |
