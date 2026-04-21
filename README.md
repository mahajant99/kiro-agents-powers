# Kiro Agents & Powers

A reference guide for the custom agents and powers configured in this Kiro workspace.

---

## Agents

Agents are specialized AI personas with focused instructions and tool access. They can be invoked directly in chat or delegated to by other agents.

### product-owner-story-writer

**Purpose**: Writes detailed, well-structured agile user stories with business context, acceptance criteria, diagrams, and success metrics.

**When to use**:
- You need to create user stories for a feature or epic
- You want acceptance criteria in Given-When-Then format
- You need supporting diagrams (sequence, ER, state, wireframes)
- You want NFRs identified and properly categorized

**How it works**:
The agent takes a question-driven approach — it asks one clarifying question at a time to fully understand the requirement before writing anything. It examines the workspace for technical context (e.g., `MASTER_TECHNICAL_SUMMARY.md`) and reviews relevant code to keep stories grounded in reality.

**Story types it handles**:
| Type | Description |
|------|-------------|
| Functional | User-facing features with direct UX impact |
| Non-Functional (NFR) | Performance, security, scalability, compliance |
| Technical | Internal engineering work, infrastructure, tech debt |

**Output structure per story**:
- Business Context
- User Story (As a / I want / So that)
- Acceptance Criteria (Given-When-Then)
- Out of Scope
- Dependencies & Assumptions
- Mockups / Diagrams
- Metrics & Success Criteria
- Non-Functional Requirements

**Tools available**: read, write, web, shell

**Example prompt**:
```
Write a user story for adding a date filter to the campaigns dashboard
```

---

## Powers

Powers bundle documentation, workflow guides, and MCP server integrations into a single installable unit. They extend Kiro with domain-specific capabilities.

### mr-confluence-docs

**Purpose**: Automatically generates structured Confluence documentation from one or more GitLab Merge Requests.

**When to use**:
- You want to document a bug fix or feature after merging an MR
- A single bug fix or feature spans multiple MRs across multiple repos
- You need to place documentation in a specific location in the Confluence page tree

**Prerequisites**:
- GitLab MCP server configured and connected
- Confluence MCP server configured and connected
- Read access to the GitLab project(s)
- Write access to the target Confluence space

**How it works**:
1. You provide MR numbers and repo names
2. The agent searches GitLab and confirms the project
3. It asks whether multiple MRs are related (combined page) or independent (separate pages)
4. You provide a Confluence URL or space key
5. The agent navigates the page tree so you can pick the exact location
6. It shows a full summary and waits for confirmation before creating anything
7. It creates structured documentation with config snippets, file lists, and GitLab links

**Documentation it generates**:

| Scenario | Output |
|----------|--------|
| Bug fix | Problem, root cause, solution, files changed, testing, impact |
| Feature | Overview, business value, implementation, architecture/API/DB changes, testing, deployment notes |

**Example prompts**:
```
Document MR !123 from my-service
```
```
Document MRs !50 from service-a and !51 from service-b - same bug fix
```
```
Document MR !123 from my-service under https://confluence.example.com/display/DEV/My+Page
```

**Available steering guides** (reference these in chat with `#`):

| File | Inclusion | Purpose |
|------|-----------|---------|
| `mr-documentation-agent.md` | Always | Main agent workflow |
| `confluence-format-helper.md` | Auto (on file match) | XHTML formatting reference |
| `multiple-mrs-guide.md` | Manual | Guide for multiple related MRs |
| `quick-reference.md` | Manual | Command reference |
| `examples.md` | Manual | Detailed workflow examples |
| `troubleshooting.md` | Manual | Common issues and solutions |

**Tips**:
- Always specify the repo name — the same MR number can exist in multiple repos
- Provide the Confluence URL upfront to skip the space selection step
- Write detailed MR descriptions for better documentation quality
- If Confluence times out, check your VPN and say "try again"

---

## Quick Reference

| Name | Type | One-liner |
|------|------|-----------|
| `product-owner-story-writer` | Agent | Writes detailed agile user stories with AC, diagrams, and NFRs |
| `mr-confluence-docs` | Power | Generates Confluence docs from GitLab MRs |
