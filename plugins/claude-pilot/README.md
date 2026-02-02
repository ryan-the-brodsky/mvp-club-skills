# Claude Pilot

Claude becomes your first user.

## The Idea

Vibe coders build fast, but often skip manual testing. **Claude Pilot** flips this—Claude uses your app like a real user would, clicking buttons, filling forms, and telling you what works (and what doesn't).

## Requirements

- **Playwright MCP** - Required for browser automation
- **iOS Simulator MCP** - Optional, for mobile app testing

## Skills

### `claude-pilot:smoke-test`
Quick sanity check. Can Claude:
- Load the app?
- See the main UI?
- Click a few buttons?
- Navigate around?

Run this before committing to catch obvious breaks.

### `claude-pilot:walkthrough`
Follow a complete user journey from your PRD:
1. Start at the entry point
2. Complete each step in the flow
3. Screenshot at each stage
4. Note any friction or confusion

### `claude-pilot:report`
Generate a **First User Report**:
- Screenshots of each screen
- What worked smoothly
- What was confusing or broken
- Suggestions for improvement

### `claude-pilot:record`
Live narration mode. Claude uses your app and talks through:
- "I see a login form..."
- "Clicking the submit button..."
- "Hmm, nothing happened. Let me check the console..."

## Part of the Work Loop

Claude Pilot powers the **Evaluate** phase:

```
Articulate → Build → Prompt → Execute → Evaluate → Iterate
                                            ↑
                                    claude-pilot tests here
```

## Best with Agent Handles

Claude Pilot works best when your app has `agent-handle` attributes on interactive elements. Run `agent-handles:audit` first to check coverage.

Without handles, Claude will fall back to:
- Text content matching
- CSS selectors
- Visual identification

These work but are less reliable than explicit handles.

## Example Usage

```
"Claude, smoke test my app"
→ claude-pilot:smoke-test

"Walk through the signup flow"
→ claude-pilot:walkthrough

"Give me a first user report"
→ claude-pilot:report

"Try using my app and tell me what you see"
→ claude-pilot:record
```
