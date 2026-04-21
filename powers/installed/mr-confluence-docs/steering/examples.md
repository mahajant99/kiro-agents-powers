---
inclusion: manual
---

# Examples: MR Documentation Workflows

## Example 1: Single Bug Fix

**You**: "Document MR !789 from my-service"

**Agent**:
1. Searches for `my-service` in GitLab → finds `group/my-service`
2. Confirms: "Found group/my-service. Is that correct?"
3. Fetches MR !789 — title: "Fix null pointer exception in execution engine"
4. Classifies as Bug Fix (keyword "fix")
5. Asks: "Where should I create the documentation? Please provide a Confluence URL or space key."
6. You: "DEV space"
7. Agent lists pages in DEV space, asks where to place it
8. You: "A — new top-level page"
9. Agent suggests title: "Bug Fix: Fix Null Pointer Exception in Execution Engine"
10. You: "yes"
11. Agent creates page and provides link

---

## Example 2: Bug Fix Across Multiple Services

**You**: "Document MRs !50, !51, !52 — they all fix the data sync bug. !50 from service-a, !51 from service-b, !52 from service-c"

**Agent**:
1. Searches and confirms all three projects
2. Fetches all three MRs
3. Detects they're related (user said "same bug")
4. Asks: "Where should I create the combined documentation?"
5. You: "https://confluence.example.com/display/DEV/Bug+Fixes"
6. Agent resolves page ID, fetches children, displays tree
7. You: "A — new child page"
8. Agent suggests: "Bug Fix: Data Sync Issue"
9. Creates one combined page with sections for each MR

**Result**: One page showing:
- Overall problem description
- How each MR contributes to the fix
- Combined testing and impact
- Links to all three MRs

---

## Example 3: Feature Across Multiple Repos

**You**: "Document !100 from service-a and !101 from service-b — they implement the new analytics feature together"

**Agent**:
1. Confirms both projects
2. Fetches both MRs
3. Classifies both as Feature
4. Asks for Confluence location
5. You: "https://confluence.example.com/display/ENG/Features"
6. Agent shows page tree, you drill down to the right section
7. Creates one combined page showing how both MRs implement the feature

---

## Example 4: Multiple Independent MRs (Sprint Release)

**You**: "Document MRs !456, !457, !458 from my-service — Sprint 42 release"

**Agent**:
1. Fetches all three MRs
2. Asks: "Are these related to the same bug/feature, or independent changes?"
3. You: "Independent — different features and fixes"
4. Agent asks: "How should I structure this? Parent page + children, or separate pages?"
5. You: "Parent page titled 'Sprint 42 Release' with child pages for each MR"
6. Agent asks for Confluence location
7. Creates parent page with summary table + 3 child pages

---

## Example 5: Feature with Config Changes

**You**: "Document MR !234 from my-service — it sets up a new environment"

**Agent**:
1. Fetches MR !234
2. Detects config files changed: `conf/new-env-service-config.json`, `conf/brand-mapping.json`
3. Classifies as Feature (new environment setup)
4. Fetches the config file contents from GitLab
5. Generates documentation including:
   - Feature description
   - Config file contents as code blocks
   - Files changed
6. Creates page with full config snippets visible

---

## Example 6: Update Existing Page

**You**: "Add MR !999 from my-service to the existing 'Q1 2026 Features' page"

**Agent**:
1. Asks for Confluence URL of the existing page
2. You: "https://confluence.example.com/display/DEV/Q1+2026+Features"
3. Agent resolves page ID, fetches current content
4. Fetches MR !999 details
5. Asks: "Should I append as a new section, or integrate into existing content?"
6. You: "New section"
7. Updates the page with MR !999 documentation appended

---

## Example 7: Drilling Down the Page Tree

**You**: "Document MR !123 from my-service under https://confluence.example.com/display/DEV/Documentation"

**Agent**:
```
Here are the pages under "Documentation":

  1. Architecture Docs
  2. API Reference
  3. Release Notes
  4. How-To Guides

Where would you like to put the documentation?

A) Create a NEW child page under "Documentation"
B) Update an EXISTING page - enter number
C) Go deeper - enter number to see children
D) Different location
```

**You**: "C3" (go deeper into Release Notes)

**Agent**:
```
Here are the pages under "Release Notes":

  1. 2025 Releases
  2. 2026 Releases
  3. Hotfixes

Where would you like to put the documentation?

A) Create a NEW child page under "Release Notes"
B) Update an EXISTING page - enter number
C) Go deeper - enter number to see children
D) Different location
```

**You**: "C2" (go deeper into 2026 Releases)

**Agent**:
```
Here are the pages under "2026 Releases":

  1. Q1 2026
  2. Q2 2026

A) Create a NEW child page under "2026 Releases"
B) Update an EXISTING page - enter number
C) Go deeper - enter number to see children
D) Different location
```

**You**: "B2" (update Q2 2026)

**Agent**: Fetches Q2 2026 page, asks how to integrate the new content, updates the page.

---

## Example 8: Handling Confluence Timeout

**You**: "Document MR !123 from my-service"

**Agent**: [Confluence times out]

```
Confluence appears to be temporarily unavailable (connection timeout).

Please check:
- VPN connection
- Try opening Confluence in your browser

Say "try again" when ready.
```

**You**: "try again"

**Agent**: Retries and continues from where it left off.
