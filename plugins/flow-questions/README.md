# Flow Questions

The right questions at the right moments.

## The Idea

Vibe coders build intuitively, but sometimes that means skipping important considerations. Flow Questions adds gentle prompts that encourage thinking about validation, edge cases, and user experience—without breaking your flow.

## How It Works

Flow Questions hooks into your development workflow and asks contextual questions at natural moments:

| Trigger | Question Type |
|---------|---------------|
| New component created | "What should a user be able to do with this?" |
| Form added | "What happens with invalid input?" |
| Multiple edits to same file | "Are we circling? Step back?" |
| Error in output | "Want me to reproduce this as a user?" |
| Long session, no commit | "Want me to test what we have?" |

## Skills

### `flow-questions:on-new-file`
Triggered after creating a new file. Asks about intent and validation.

### `flow-questions:on-edit`
Triggered after edits. Detects patterns (forms, buttons, error handling) and asks relevant questions.

### `flow-questions:prompt-me`
Manually request a validation prompt:
```
"Ask me something about this code"
"What should I be thinking about?"
"Prompt me"
```

### `flow-questions:configure`
Adjust frequency and types of questions:
```
"Too many questions, tone it down"
"Ask more about error handling"
"Only prompt before commits"
```

## Example Prompts

### After Creating a Form Component
> "Nice! A signup form. Quick questions:
> - What happens if someone submits with empty fields?
> - What about an already-registered email?
> - Want me to try it once it's hooked up?"

### After Multiple Edits to Same File
> "I notice we've edited this file 8 times in the last 20 minutes.
> Sometimes that means we're circling on something tricky.
> Want to step back and re-articulate what we're trying to do?"

### After Adding Error Handling
> "Good error handling! Just checking:
> - Does the user see a helpful message?
> - Can they recover from this state?
> - Want me to trigger this error path and screenshot it?"

### Before a Long Session Ends
> "We've been building for a while. Before we stop:
> - Want me to smoke test what we have?
> - Should I capture screenshots for the journal?
> - Anything we should note in the PRD?"

## Configuration

Control question behavior:

```json
{
  "flow-questions": {
    "frequency": "moderate",
    "triggers": {
      "new-file": true,
      "forms": true,
      "errors": true,
      "circling": true,
      "long-session": true
    },
    "quiet-mode": false
  }
}
```

### Frequency Levels
- **minimal** - Only critical moments
- **moderate** - Balanced prompts (default)
- **active** - Frequent guidance
- **quiet** - Disabled (manual only)

## Philosophy

- **Guide, don't interrupt** - Questions should feel helpful, not nagging
- **Context-aware** - Ask about forms when they create forms, not randomly
- **Optional** - Always easy to dismiss or disable
- **Actionable** - Questions should lead somewhere useful

## Part of the Work Loop

Flow Questions embeds **Evaluate** thinking throughout the **Build** phase:

```
Articulate → Build → Prompt → Execute → Evaluate → Iterate
               ↑                           ↑
         questions here              and here
```

Instead of saving all evaluation for the end, Flow Questions encourages continuous validation thinking.
