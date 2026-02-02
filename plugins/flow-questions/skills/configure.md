---
name: configure
description: Use this skill to adjust flow question frequency and types. Activate when users say "too many questions", "change question settings", "configure prompts", "adjust flow questions". Invoke with flow-questions:configure.
---

# Flow Questions: Configure

You are helping the user adjust how and when Flow Questions prompts them.

## Default Configuration

```json
{
  "flow-questions": {
    "frequency": "moderate",
    "triggers": {
      "new-file": true,
      "forms": true,
      "errors": true,
      "circling": true,
      "destructive-actions": true,
      "long-session": true
    },
    "cooldown-minutes": 5,
    "quiet-hours": null
  }
}
```

## Configuration Options

### Frequency
How often questions appear:

| Level | Behavior |
|-------|----------|
| `minimal` | Only critical moments (circling, destructive actions) |
| `moderate` | Balanced prompts for forms, errors, patterns |
| `active` | Frequent guidance for learning/complex work |
| `quiet` | Manual only (`prompt-me` still works) |

### Triggers
Enable/disable specific prompt triggers:

| Trigger | What It Detects |
|---------|-----------------|
| `new-file` | Creating new components |
| `forms` | Form fields added/edited |
| `errors` | Error handling added |
| `circling` | Repeated edits to same file |
| `destructive-actions` | Delete/remove operations |
| `long-session` | Extended work without commits |
| `api-calls` | New fetch/API code |
| `loading-states` | Loading UI added |

### Cooldown
Minimum minutes between automatic prompts:
- Default: 5 minutes
- Lower for learning mode
- Higher for experienced developers

### Quiet Hours
Disable automatic prompts during focus time:
```json
{
  "quiet-hours": {
    "start": "14:00",
    "end": "16:00"
  }
}
```

## Configuration Process

### 1. Understand the Issue
Ask what's not working:
- "Are questions too frequent?"
- "Not relevant to what you're building?"
- "Want more guidance in certain areas?"

### 2. Propose Changes

Based on feedback:

**"Too many questions"**
```json
{
  "frequency": "minimal",
  "cooldown-minutes": 15
}
```

**"Questions aren't relevant"**
```json
{
  "triggers": {
    "new-file": false,
    "forms": true,
    "errors": true,
    "circling": true
  }
}
```

**"I want more guidance"**
```json
{
  "frequency": "active",
  "cooldown-minutes": 3
}
```

**"Only bug me about important stuff"**
```json
{
  "frequency": "minimal",
  "triggers": {
    "circling": true,
    "destructive-actions": true,
    "forms": false,
    "new-file": false
  }
}
```

### 3. Apply and Confirm

```markdown
Updated Flow Questions configuration:

**Frequency:** minimal
**Active triggers:** circling, destructive-actions
**Cooldown:** 15 minutes

You'll see fewer prompts now. You can always use `flow-questions:prompt-me`
to get a question manually, or adjust settings with `flow-questions:configure`.
```

## Quick Adjustments

Common requests and responses:

**"Tone it down"**
```markdown
Got it. Switching to minimal frequency with 15-minute cooldown.
You'll only get questions for repeated edits or destructive actions.
```

**"Turn off the questions"**
```markdown
Understood. Setting to quiet mode.

Automatic prompts are now off. You can still use `flow-questions:prompt-me`
anytime you want a validation check.
```

**"I want more help"**
```markdown
Sure! Switching to active mode with all triggers enabled.

You'll get questions when you:
- Create new components
- Add forms, error handling, or API calls
- Edit the same file repeatedly
- Add destructive actions

Let me know if it's too much.
```

**"Only ask about forms"**
```markdown
Done. Disabling all triggers except forms.

I'll only prompt when you add or edit form-related code.
```

## Where Configuration Lives

Save configuration in:
- `.claude/flow-questions.json` (preferred)
- Project's `claude.config.json` under `flow-questions`

## Reset to Defaults

```markdown
Reset Flow Questions to defaults?

This will set:
- Frequency: moderate
- All triggers: enabled
- Cooldown: 5 minutes

Confirm?
```

## Tone

Be accommodating. Prompt frequency is personal preference—there's no wrong answer. Help them find what works for their workflow without judgment.
