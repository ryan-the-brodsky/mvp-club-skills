---
name: on-edit
description: This skill triggers automatically (via hook) after editing files, detecting patterns that warrant questions. Notices things like repeated edits, form additions, error handling changes.
---

# Flow Questions: On Edit

You are observing edit patterns and prompting with relevant questions when it would be helpful. The goal is to catch moments where a question might prevent issues or improve thinking.

## Trigger

This skill activates:
- Automatically via `PostToolUse` hook on `Edit`
- Only triggers when patterns are detected (not on every edit)

## Pattern Detection

### Repeated Edits (Circling)
**Trigger:** Same file edited 5+ times in short period

```markdown
I notice we've edited `[filename]` quite a few times now.

This sometimes means we're working through something tricky. Options:
- **Keep going** - You've got this, just iterating
- **Step back** - Want to re-articulate what we're trying to do?
- **Test it** - Want me to try using what we have so far?

No pressure—just checking in.
```

### Form Field Added
**Trigger:** Edit adds `<input>`, `<select>`, `<textarea>`, or form-related code

```markdown
New form field spotted.

Quick validation check:
- Is this field required or optional?
- Any format restrictions? (email, phone, length)
- What error message should users see?

Form validation is one of those things that's easier to think through now than debug later.
```

### Error Handling Added
**Trigger:** Edit adds `try/catch`, `.catch()`, error state, or error message

```markdown
Good—error handling!

Making sure it's user-friendly:
- Does the error message help users understand what happened?
- Can they recover from this state? (retry, go back)
- Should we log this for debugging?

Want me to try triggering this error path?
```

### Loading State Added
**Trigger:** Edit adds loading spinner, skeleton, `isLoading`, etc.

```markdown
Loading state added.

UX consideration:
- How long before it feels "stuck"? (>3s usually needs feedback)
- What if it never finishes? (timeout handling)
- Is there a way to cancel?

Small thing, but loading states really affect how the app feels.
```

### API Call Added
**Trigger:** Edit adds `fetch`, `axios`, API route call

```markdown
New API call.

Quick checks:
- What happens if the network is slow?
- What about if it fails entirely?
- Is there sensitive data that needs protection?

When this is wired up, I can test the happy path and failure modes.
```

### Button/Click Handler Added
**Trigger:** Edit adds `onClick`, button with action

```markdown
New click action.

Feedback considerations:
- Does clicking show something is happening?
- Should it be disabled during processing?
- What if the user double-clicks?

Consider adding `agent-handle` for automated testing.
```

### Delete/Destructive Action Added
**Trigger:** Edit adds delete, remove, or destructive operation

```markdown
Destructive action detected.

Safety check:
- Is there a confirmation dialog?
- Can this be undone?
- What feedback shows it worked?

These are high-stakes interactions—worth getting right.
```

## When NOT to Trigger

- Config/boilerplate changes
- Import statements only
- Comment changes
- Formatting/whitespace
- Test file edits
- If last question was < 5 minutes ago (avoid nagging)

## Frequency Control

Respect configuration:
- `frequency: minimal` - Only trigger for circling detection
- `frequency: moderate` - Trigger for forms, errors, destructive actions
- `frequency: active` - Trigger for most patterns
- `frequency: quiet` - Don't trigger automatically

## Session Context

Track session state to ask better questions:

- **Edit count per file** - Detect circling
- **Time since last prompt** - Avoid over-prompting
- **Types of components touched** - Understand the work

## Tone

Observational and supportive. You're noticing patterns, not catching mistakes.

```markdown
// Good
"I notice we've been iterating on this form quite a bit.
Sometimes it helps to step back—want to talk through what we're trying to achieve?"

// Too critical
"You've edited this file 8 times. That's a lot.
Are you sure you know what you're doing?"
```

## Dismissal

Always make it easy to dismiss:
- "Got it, keep going"
- "I'll think about that"
- "Not now"

These are suggestions, not requirements.
