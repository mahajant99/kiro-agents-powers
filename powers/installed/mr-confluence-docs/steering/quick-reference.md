---
inclusion: manual
---

# Quick Reference: MR Documentation Commands

## Basic Commands

### Single MR
```
Document MR !123 from my-service
Document MR !123 from my-service on Confluence
Create docs for MR !123 from my-service
```

### Multiple MRs — Same Bug/Feature
```
Document MRs !123, !124 - they fix the same bug
!123 from service-a, !124 from service-b - same feature
```

### Multiple MRs — Independent
```
Document MRs !123 from service-a and !124 from service-b
Create separate docs for !123 from service-a and !124 from service-b
```

### With Confluence URL
```
Document MR !123 from my-service under https://confluence.example.com/display/DEV/My+Page
```

### With Space Key
```
Document MR !123 from my-service in DEV space
```

### Update Existing Page
```
Update the existing "Sprint 42" page with MR !123 from my-service
Add MR !123 from my-service to the existing "Release Notes" page
```

### Custom Classification Override
```
Document MR !123 from my-service as a feature
Document MR !123 from my-service as a bug fix
```

## Confluence Page Tree Navigation

When the agent shows the page tree:
- Enter **A** to create a new child page at the current level
- Enter **B + number** to update an existing page (e.g., "B2")
- Enter **C + number** to drill deeper into a child page (e.g., "C3")
- Enter **D** to provide a different URL

## GitLab MCP Tools Used

| Tool | Purpose |
|------|---------|
| `mcp_gitlab_search_projects` | Find project by repo name |
| `mcp_gitlab_get_merge_request` | Get MR details |
| `mcp_gitlab_get_file` | Get file contents for config snippets |
| `mcp_gitlab_list_branches` | List branches |

## Confluence MCP Tools Used

| Tool | Purpose |
|------|---------|
| `mcp_confluence_confluence_create_page` | Create new page (requires numeric parent_id) |
| `mcp_confluence_confluence_update_page` | Update existing page |
| `mcp_confluence_confluence_get_page_children` | List child pages WITH their IDs |
| `mcp_confluence_confluence_get_space_content` | List space pages WITH their IDs |
| `mcp_confluence_confluence_get_page` | Get page content (does NOT return numeric ID) |
| `mcp_confluence_confluence_search` | Search for pages |
| `mcp_confluence_confluence_list_spaces` | List available spaces |

## Page ID Resolution Methods

The `create_page` tool needs a numeric `parent_id`. Get it by:

1. **From URL**: Extract `pageId=XXXXXXX` if present in the URL
2. **From space content**: `get_space_content` returns pages with IDs
3. **From page children**: `get_page_children` returns children with IDs
4. **From page HTML**: Look for `data-pageid="XXXXXXX"` in the HTML content
