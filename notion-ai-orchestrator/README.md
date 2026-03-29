# Notion AI Orchestrator

A Claude skill that orchestrates Notion AI through the [Claude Chrome Extension](https://chromewebstore.google.com/detail/claude-in-chrome/kjaflnafmkmchboheegfcnilkpddmmgd), enabling Claude to delegate workspace-level actions to Notion's built-in AI agent by controlling its chat interface programmatically.

## What It Does

Instead of using Notion's API directly, this skill lets Claude interact with Notion AI the same way a human would — through its chat interface. This unlocks capabilities that only Notion's native AI agent has permission to perform:

- **Create databases** with complex property schemas, views, and filters
- **Search across an entire workspace** — journal entries, notes, databases, everything
- **Bulk-organize pages** and restructure content
- **Modify existing pages and databases** by name
- **Summarize and analyze** workspace content

## Demo

Watch the full walkthrough of the Notion AI Orchestrator in action:

[Loom Video Walkthrough](https://www.loom.com/share/0580d68146b745bcb73bdb1f2191aa53)

## Prerequisites

- Claude Chrome Extension active with a browser tab open to notion.so
- Logged into your Notion workspace
- Notion AI enabled in the workspace

## Quick Start

1. Copy the `notion-ai-orchestrator/` folder to `~/.claude/skills/`
2. Open a Notion tab in Chrome
3. Ask Claude: *"Use Notion AI to create a project tracker database"*

## How It Works

The skill follows a 7-step workflow:

1. Navigate to the Notion AI chat in the sidebar
2. Focus the contenteditable input field (via ref-click, not coordinates)
3. Type the prompt
4. Submit via the send button
5. Wait for completion (10s to 2+ min depending on complexity)
6. Read and parse the response
7. Optionally follow up in the same thread

See [SKILL.md](./SKILL.md) for the full implementation details, prompt crafting guidelines, and error handling reference.

## Example Prompts

- *"Search through all of my workspace for anything related to Q1 goals"*
- *"Create a CRM database with Status, Company, Contact, Deal Size, and Next Steps columns"*
- *"Organize all my meeting notes from January into a single summary page"*

## Links

- [Skill Ecosystem](https://github.com/mrtblount/skill-ecosystem) — Framework and builder tools
- [tonyblount.com](https://tonyblount.com) — Portfolio
- [Four30.co](https://four30.co) — Consulting
- [LinkedIn](https://www.linkedin.com/in/williamblount/)
