# MR Confluence Documentation Power

## Overview
Automatically generate comprehensive Confluence documentation from GitLab Merge Requests. This power analyzes MR changes, classifies them as bugs or features, and creates structured documentation on Confluence.

## Keywords
- mr-docs
- confluence-docs
- merge-request-documentation
- gitlab-confluence
- auto-documentation
- mr-to-confluence
- document mr
- document merge request

## Description
This power streamlines the documentation process by:
1. Asking for repo names and resolving GitLab project paths
2. Fetching MR details and file changes
3. Analyzing changes to classify as bug fixes or new features
4. Navigating the Confluence page tree so you can pick exactly where to place docs
5. Generating appropriate documentation structure
6. Creating or updating Confluence pages with the documentation

## Use Cases
- Document a single MR as a bug fix or feature
- Document multiple related MRs as one combined page (e.g., a bug fix spanning multiple repos)
- Document multiple independent MRs as separate pages
- Navigate Confluence page hierarchy to place docs in the right location
- Update existing Confluence pages with new MR information

## Prerequisites
- GitLab MCP server configured and connected
- Confluence MCP server configured and connected
- Access to the GitLab project(s)
- Write permissions to the target Confluence space

## How to Use

### Basic Usage
```
Document MR !123 from my-service
```

### Multiple MRs (same bug/feature)
```
Document MRs !123 from service-a and !124 from service-b - same bug fix
```

### Multiple Independent MRs
```
Create Confluence docs for !123 from service-a and !124 from service-b
```

### With Confluence URL
```
Document MR !123 from my-service under https://confluence.example.com/display/DEV/My+Page
```

## What the Agent Does

1. **Asks for repo names** - mandatory for every MR (same number can exist in multiple repos)
2. **Searches GitLab** - finds the project automatically, confirms with you
3. **Asks if MRs are related** - determines whether to create one combined page or separate pages
4. **Navigates Confluence** - fetches and displays the page tree so you can drill down and pick the exact location
5. **Classifies changes** - determines bug fix vs feature from MR content
6. **Generates documentation** - creates structured docs with config snippets, file lists, and links
7. **Confirms before creating** - shows a full summary and waits for your yes/no

## What Gets Documented

### For Bug Fixes
- Problem description and symptoms
- Root cause analysis (if available)
- Solution implemented
- Files changed (with config snippets if applicable)
- Testing approach
- Impact assessment

### For Features
- Feature overview and purpose
- Business value (if available)
- Implementation approach
- Architecture / API / Database changes (if applicable)
- Configuration changes (with snippets)
- Files modified
- Testing strategy
- Deployment notes

## Tips
- Include detailed MR descriptions for better documentation quality
- Use conventional commit messages for better classification
- Link issue tickets in MRs for automatic cross-referencing
- Provide the Confluence URL upfront to skip the space selection step
- If Confluence times out, check your VPN and say "try again"
