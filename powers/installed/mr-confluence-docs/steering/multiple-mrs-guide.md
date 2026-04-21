---
inclusion: manual
---

# Multiple MRs for Single Bug or Feature

## When to Use This

A single bug fix or feature often requires changes across multiple repositories:

- **Bug fix across multiple services**: One bug affecting multiple services, each needing a fix
- **Feature split into parts**: Large feature implemented across multiple MRs for easier review
- **Bug fix with follow-up**: Initial fix + additional improvements or corrections
- **Cross-service feature**: New capability requiring changes in multiple projects

## How to Request

Be explicit about the relationship:

```
Document MRs !123, !124, !125 - they all fix the login timeout bug
!123 from service-a, !124 from service-b, !125 from service-c
```

```
Document !100, !101, !102 - parts 1, 2, 3 of the new analytics feature
!100 from service-a, !101 from service-b, !102 from service-a
```

## Documentation Options

### Option 1: Single Combined Page (recommended for related MRs)

Best when: All MRs together solve one problem or implement one feature

**Structure**:
```markdown
# [Bug Fix / Feature]: [Overall Description]

## Overview
- Related MRs: ![number] (repo-a), ![number] (repo-b)
- Type: Bug Fix / Feature
- Status: All Merged

## Summary
[What problem was solved / what capability was added]

## Solution Approach
[How the MRs together solve the problem]

---

## MR ![number] — [repo-name]
- Author: [name]
- Contribution: [what this MR specifically does]
### Changes
- `path/to/file` - [what changed]

---

## MR ![number] — [repo-name]
- Author: [name]
- Contribution: [what this MR specifically does]
### Changes
- `path/to/file` - [what changed]

---

## Combined Testing
[Testing across all MRs]

## Impact
- Affected Services: [list]
- User Impact: [description]

## Related Links
- MR ![number]: [URL]
- MR ![number]: [URL]
```

### Option 2: Parent Page + Child Pages

Best when: Each MR has substantial independent changes worth their own page

**Structure**:
- Parent page: Overview, summary table, architecture
- Child pages: Detailed docs for each MR

### Option 3: Update Existing Page

Best when: Adding a follow-up MR to existing documentation

```
Add MR !999 from my-service to the existing "Login Timeout Fix" page
```

## Agent Behavior

When you provide multiple MRs, the agent asks:

```
I have [N] MRs to document:
- ![number] from [repo-a]
- ![number] from [repo-b]

Are these MRs:
1. All related to the same bug or feature? -> one combined page
2. Separate independent changes? -> separate pages
3. Part of a larger initiative? -> parent page with child pages
```

### Clues the agent uses to detect related MRs

- You say "they all fix...", "same bug", "same feature", "together"
- Similar titles or descriptions across MRs
- Same issue/ticket referenced in multiple MRs
- Same source branch across repos

## Tips

**Specify projects upfront** to save time:
```
!123 from service-a, !124 from service-b — same bug fix
```

**State the relationship clearly**:
- ✅ "they all fix the login bug"
- ✅ "parts 1, 2, 3 of the analytics feature"
- ✅ "initial fix + follow-up correction"

**For config-heavy MRs**: The agent will fetch and include config file contents as code blocks automatically when it detects config files in the changed files list.
