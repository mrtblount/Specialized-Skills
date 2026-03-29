---
name: notion-ai-orchestrator
description: >
  Orchestrate Notion AI through the Claude Chrome Extension. Delegates workspace-level
  actions (creating databases, searching content, modifying pages, setting up automations)
  to Notion's built-in AI agent by controlling its chat interface programmatically.
  Triggers: "notion ai", "create notion database", "search notion", "organize notion",
  "notion workspace", "use notion ai to", "ask notion ai".
---

<role>
Notion AI Orchestrator — controls the Notion AI chat interface through the Claude Chrome
Extension, enabling Claude to delegate workspace-level actions to Notion's built-in AI agent.

The workflow: open the Notion AI chat, type a prompt, submit it, wait for execution,
and read back results. This lets Claude use Notion AI as a tool for actions only the
Notion AI agent has permission to perform.
</role>

<context>
**Prerequisites** (all three must be true):
- Claude Chrome Extension is active with a browser tab open to notion.so
- User is logged into their Notion workspace
- Notion AI is enabled in the workspace

**What Notion AI can do:**
- Create databases with complex property schemas
- Search across an entire workspace
- Bulk-organize pages
- Set up views and filters
- Summarize or analyze workspace content
- Modify existing pages and databases

**What Notion AI cannot do:**
- Create database page templates or Notion automations (documents setup instructions instead)
- Set database descriptions via its tools (provides text to paste manually)
- Read text inside embedded images
- Guarantee complete results on very large workspaces (narrow the search scope if incomplete)
</context>

<instructions>

## Step 1: Navigate to Notion AI Chat

Click the **"Notion AI"** link in the upper portion of the left sidebar (below "Meetings", above "Inbox"). This opens a full-page chat interface.

**Fallback:** If the sidebar link is not visible, look for the Notion AI mascot icon (round face with a small cat on top) in the bottom-right corner and click it.

```
Action: left_click on "Notion AI" sidebar link
Expected: Full-page chat loads at notion.so/ai with heading "Meow... what's your request?"
```

## Step 2: Focus the Text Input

**CRITICAL:** The input field is a `contenteditable` div, NOT a standard input or textarea. You **cannot** use `form_input`. You **must** use ref-based clicking.

```
Action: find(query="Do anything with AI textbox") → get ref
Action: left_click(ref=<returned_ref>)
```

**Never** attempt to type before clicking via ref — the type action will not register unless the field is focused through its element reference. Coordinate-based clicks are unreliable for this element.

## Step 3: Type the Prompt

Once focused via ref-click, use the `type` action to enter the prompt.

```
Action: type(text="Your full prompt here")
```

**Formatting rules:**
- Type the entire prompt as continuous text — **Enter submits the message**
- For line breaks within the prompt, use **Shift+Return**
- For very long prompts, type in chunks separated by Shift+Return twice
- Keep prompts clear, specific, and action-oriented with exact names for properties, options, views, etc.

**If typing fails** (placeholder still showing): The ref-click did not properly focus the field. Re-run `find` to get a fresh ref, click it again, then retry typing.

## Step 4: Submit the Prompt

```
Action: find(query="Submit AI message button") → get ref
Action: left_click(ref=<returned_ref>)
```

The chat transitions: your message appears as sent, the page title updates, and Notion AI begins working. Status indicators appear ("Crafting", "Creating database", step checkmarks, etc.).

## Step 5: Wait for Completion

Notion AI tasks take 10 seconds to 2+ minutes depending on complexity.

**Monitoring loop:**
1. `wait(duration=15)` after submitting
2. `screenshot` to check progress
3. Look for completion indicators:
   - Full prose response with no spinning indicators
   - Action buttons at bottom (copy, thumbs up/down, "Contact Notion support", "Undo")
   - Step list showing all checkmarks completed
   - Input field at bottom is idle (no stop button visible)
4. If still processing: `wait(duration=20)` then `screenshot` again
5. Scroll down if needed — long responses extend below the viewport

## Step 6: Read the Response

Scroll through the response to read it. For long responses, use `scroll(direction="down")` at the center of the chat area.

**Response may include:**
- Confirmation of what was built or found
- Links to created pages/databases (clickable refs)
- Items requiring manual setup (clearly documented by Notion AI)
- Summaries of searched content
- Step-by-step instructions for anything it couldn't automate

To capture full response text: `get_page_text` on the tab (note: captures entire page including sidebar).

## Step 7: Follow Up (Optional)

The input field resets to empty after completion. Send follow-up messages in the same thread to refine results or request modifications — repeat Steps 2-6.

For a completely new/unrelated task, navigate back to Notion AI (Step 1) for a fresh chat.

</instructions>

<reference topic="prompt-crafting">
## Prompt Crafting Guidelines

**Database Creation:**
- Specify exact database name and placement (e.g., "under Private in the sidebar")
- List every property with its exact type (Select, Multi-Select, Checkbox, Date, Number, Rich Text, URL, Files & Media)
- List every Select/Multi-Select option explicitly
- Define each view by name, type (table/board/gallery), filters, sorts, and visible columns
- Note: Templates and automations cannot be created programmatically — Notion AI documents the specs for manual setup

**Searching / Summarizing:**
- Tell it to search broadly: "Search through all of my workspace — journal entries, notes, databases, everything."
- Be specific about what to extract: dates, quotes, context, dosages, takeaways, etc.
- Cannot read text inside embedded images

**Modifying Existing Content:**
- Reference pages and databases by their exact names
- Be explicit about what to change, add, or remove
</reference>

<reference topic="quick-reference">
## Quick Reference

```
1. left_click "Notion AI" in sidebar        → notion.so/ai
2. find("Do anything with AI textbox")       → ref
3. left_click(ref)                           → focus input
4. type("Your prompt")                       → enter text
5. find("Submit AI message button")          → ref
6. left_click(ref)                           → submit
7. wait(15) → screenshot → check completion  → repeat if needed
8. scroll down → read full response
```
</reference>

<error_handling>
| Problem | Cause | Fix |
|---------|-------|-----|
| Typing doesn't register | Input not focused via ref | Re-run `find`, get fresh ref, click again |
| Placeholder still showing after type | Ref-click failed to focus | Get new ref, click, retry |
| `form_input` fails | Input is contenteditable div | Use `find` + `left_click(ref)` + `type` instead |
| Coordinate-based click misses | Contenteditable elements shift | Always use ref-based clicks |
| Response seems incomplete | Large workspace, partial results | Narrow search scope and retry |
| Notion AI says it can't create templates | Known limitation | Accept documented setup instructions |
</error_handling>
