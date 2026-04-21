# MR Confluence Documentation Power

Automatically generate comprehensive Confluence documentation from GitLab Merge Requests.

## Key Principles

- **Repo name is mandatory** for every MR (same number can exist in multiple repos)
- **Navigate the page tree** — agent fetches and displays child pages so you pick the exact location
- **Ask, don't assume** — agent asks questions until it has complete information
- **Multiple MRs = one story** — a bug fix or feature can span multiple MRs across multiple repos

## Quick Start

```
Document MR !123 from my-service
```

```
Document MRs !123 from service-a and !124 from service-b - same bug fix
```

```
Document MR !123 from my-service under https://confluence.example.com/display/DEV/My+Page
```

## How It Works

1. **You provide**: MR numbers + repo names
2. **Agent searches**: Finds the GitLab project automatically
3. **Agent asks**: Are these MRs related? (combined page or separate?)
4. **You provide**: A Confluence URL or space key
5. **Agent navigates**: Fetches and displays the page tree — you drill down to the exact location
6. **Agent confirms**: Shows a full summary before creating anything
7. **Agent creates**: Structured documentation with config snippets, file lists, and GitLab links

## Page Tree Navigation

When you provide a Confluence URL, the agent will:

```
Here are the pages under "My Section":

  1. Sub-section A - [URL]
  2. Sub-section B - [URL]
  3. Sub-section C - [URL]

Where would you like to put the documentation?

A) Create a NEW child page here
B) Update an EXISTING page - enter number
C) Go deeper - enter number to see children
D) Different location
```

You can drill down as many levels as needed.

## Multiple MRs for Same Bug/Feature

A single bug fix or feature often spans multiple MRs across multiple repos:

```
Document MRs !50, !51, !52 - they all fix the data sync bug
!50 from service-a, !51 from service-b, !52 from service-c
```

The agent creates **one combined page** showing:
- Overall problem/feature description
- How each MR contributes
- Combined testing and impact
- Links to all MRs

## Documentation Structures

| Scenario | Structure |
|----------|-----------|
| Single MR | One page |
| Multiple related MRs (same bug/feature) | One combined page |
| Multiple independent MRs | Separate pages or parent + children |
| Large phased feature | Parent page + child pages per phase |

## What Gets Documented

### Bug Fixes
- Problem description and symptoms
- Root cause (if available in MR)
- Solution implemented
- Files changed (with config snippets if applicable)
- Testing approach
- Impact assessment

### Features
- Feature overview and purpose
- Business value (if available)
- Implementation approach
- Architecture / API / Database / Config changes
- Files modified
- Testing strategy
- Deployment notes

## Prerequisites

- GitLab MCP server configured and connected
- Confluence MCP server configured and connected
- Access to GitLab projects
- Write permissions to Confluence spaces

## Tips

- Provide the Confluence URL upfront to skip space selection
- Be explicit about MR relationships: "they all fix the same bug"
- Specify repo names upfront: "!123 from service-a, !124 from service-b"
- If Confluence times out, check your VPN and say "try again"
- Write detailed MR descriptions for better documentation quality

## Troubleshooting

### "Which project is this MR from?"
Multiple repos can have the same MR number — always specify the repo

### Page ID issues
If the agent can't find a page, provide the URL with `pageId=XXXXXXX` format for reliable resolution

## Available Steering Files

| File | Inclusion | Purpose |
|------|-----------|---------|
| `mr-documentation-agent.md` | Always | Main agent workflow |
| `confluence-format-helper.md` | Auto | XHTML formatting reference |
| `multiple-mrs-guide.md` | Manual | Guide for multiple related MRs |
| `quick-reference.md` | Manual | Command reference |
| `examples.md` | Manual | Detailed workflow examples |
| `troubleshooting.md` | Manual | Common issues and solutions |
