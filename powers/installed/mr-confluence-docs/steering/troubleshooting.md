---
inclusion: manual
---

# Troubleshooting Guide

## Confluence Issues

### Confluence times out / JSON parse error

**Symptoms**: `Read timed out`, `Expecting value: line 3 column 1`, `HTTPSConnectionPool`

**Cause**: Intermittent connectivity to the Confluence server (often VPN-related)

**Fix**:
1. Check your VPN connection
2. Try opening Confluence in your browser to confirm it's accessible
3. Say "try again" — the agent will retry the operation

---

### Cannot find numeric page ID

**Symptom**: Agent can't resolve the page ID needed for `parent_id`

**Cause**: `mcp_confluence_confluence_get_page` returns page content but NOT the numeric ID

**Fix options**:
1. Provide a URL with `pageId=XXXXXXX` format — the ID is in the URL
   - Example: `https://confluence.example.com/pages/viewpage.action?pageId=12345`
2. The agent will use `get_space_content` to list pages with IDs and match by title
3. If all else fails, open the page in your browser, click `...` → Page Information to find the ID

---

### Page already exists with same title

**Error**: "Page with title 'X' already exists in space"

**Fix**:
- Ask the agent to update the existing page instead:
  ```
  Update the existing "My Page" with MR !123
  ```
- Or use a different title:
  ```
  Create page titled "My Page - v2" for MR !123
  ```

---

### Confluence space not found

**Error**: "Space 'XYZ' not found"

**Fix**:
- Space keys are case-sensitive
- Ask the agent to list available spaces:
  ```
  What Confluence spaces are available?
  ```
- Provide the exact space key from the list

---

## GitLab Issues

### MR not found

**Error**: "Merge request !123 not found"

**Possible causes**:
- Wrong repo name
- MR number incorrect
- No access to the project

**Fix**:
- Verify the MR number in GitLab UI
- Specify the full project path:
  ```
  Document MR !123 from group/subgroup/my-service
  ```
- Check GitLab access permissions

---

### Multiple projects have the same MR number

**Scenario**: Agent asks "which project?" for MR !123

**Why**: Multiple repositories can have MR !123 — this is expected

**Fix**: Always specify the repo name:
```
Document MR !123 from service-a and MR !123 from service-b
```

---

### GitLab rate limit exceeded

**Error**: "Rate limit exceeded"

**Fix**:
- Wait a few minutes
- Process MRs in smaller batches
- Check GitLab token permissions

---

## Classification Issues

### Agent can't determine bug vs feature

**Scenario**: MR has mixed indicators

**Agent behavior**: Explains its analysis and asks you to decide:
```
MR !123 has mixed indicators:
- Bug indicators: title mentions "fix", modifies existing error handling
- Feature indicators: adds new retry mechanism, creates new classes

Should I classify this as:
1. Bug Fix
2. Feature
```

**Fix**: Simply reply with your choice (1 or 2)

---

### Wrong classification

**Fix**: Override it explicitly:
```
Document MR !123 from my-service as a feature
```

---

## Documentation Quality Issues

### MR has no description

**Agent behavior**: States "Not provided in MR description" and infers from code changes

**Fix**: Add a description to the MR in GitLab, then re-run

---

### Config files not shown in docs

**Fix**: The agent fetches config files when it detects them in the changed files list. If a specific config file is missing, ask:
```
Include the contents of conf/my-config.json in the documentation
```

---

### Large MR with too many files

**Agent behavior**: Groups files by category and summarizes

**Fix**: If you want specific files highlighted, mention them:
```
Focus on the changes to DatabaseConfig.java and ServiceConfig.json
```

---

## Debugging Commands

```
# Check GitLab connection
List my GitLab projects

# Check Confluence connection
List available Confluence spaces

# Verify MR details before documenting
Show me details of MR !123 from my-service

# Test classification without creating docs
Analyze MR !123 from my-service and tell me if it is a bug or feature, do not create docs yet

# Find a Confluence page ID
What is the page ID of https://confluence.example.com/display/DEV/My+Page
```
