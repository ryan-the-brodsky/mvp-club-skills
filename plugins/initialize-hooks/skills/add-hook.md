---
name: add-hook
description: Add a single hook to your Claude Code settings. Specify the hook by ID. Invoke with initialize-hooks:add-hook <hook-id>.
---

# Initialize Hooks: Add Hook

You are adding a single hook to the user's Claude Code settings.

## Process

### Step 1: Parse Arguments

Check if the user specified a hook ID:
- `initialize-hooks:add-hook pre-push` → Add pre-push hook
- `initialize-hooks:add-hook` (no argument) → Show available hooks and ask

### Step 2: Read Hook Definitions

Read the hook definitions from the source of truth:

```
Read: recommended-hooks.json (from the mvp-club-skills repository root)
```

### Step 3: If No Hook ID Provided

Show available hooks and ask the user to choose:

```markdown
## Available Hooks

| Hook ID | Name | Trigger |
|---------|------|---------|
| `pre-commit` | Pre-Commit Validation | Before `git commit` |
| `pre-push` | Pre-Push Validation | Before `git push` |
| `pre-pr` | Pre-PR Validation | Before `gh pr create` |
| `flow-questions` | Flow Questions | After `Write`/`Edit` |
| `prd-sync` | PRD Sync | End of session |

Which hook would you like to add?
```

Use AskUserQuestion to get their choice.

### Step 4: Validate Hook ID

If a hook ID was provided, validate it exists in `recommended-hooks.json`.

If invalid:
```markdown
Unknown hook: `invalid-hook`

Available hooks:
- `pre-commit` - Pre-Commit Validation
- `pre-push` - Pre-Push Validation
- `pre-pr` - Pre-PR Validation
- `flow-questions` - Flow Questions
- `prd-sync` - PRD Sync

Try: `initialize-hooks:add-hook pre-push`
```

### Step 5: Check Current Settings

Read `~/.claude/settings.json` to check:
1. Does the settings file exist?
2. Is the hook already configured?

If already configured:
```markdown
The **pre-push** hook is already in your settings.

Current configuration:
- Trigger: Before `git push`
- Action: `build-checkpoint:pre-push`

No changes needed. To reconfigure, use:
- `initialize-hooks:remove-hook pre-push` then add again
```

### Step 6: Show What Will Be Added

```markdown
## Adding: Pre-Push Validation

**Trigger:** Before `git push`
**Action:** Runs `build-checkpoint:pre-push`
**Purpose:** Validates your code before pushing to main

This hook will be added to `~/.claude/settings.json`.

Proceed? (yes/no)
```

### Step 7: Confirm

Use AskUserQuestion to confirm before modifying settings.

### Step 8: Add Hook

If confirmed:
1. Read current `~/.claude/settings.json` (or create if doesn't exist)
2. Get the hook config from `recommended-hooks.json`
3. Merge the hook into the appropriate section (PreToolUse, PostToolUse, or Stop)
4. Write the updated settings file

### Step 9: Confirm Success

```markdown
## Hook Added

**Pre-Push Validation** is now active.

Next time you run `git push`, validation will run automatically.

### Related Commands
- `initialize-hooks:profiles` - See all available profiles
- `initialize-hooks:remove-hook pre-push` - Remove this hook
- `build-checkpoint:skip` - Temporarily skip validation
```

## Error Handling

### Settings File Doesn't Exist

Create `~/.claude/settings.json` with just this hook.

### Invalid JSON in Settings

Show the error and offer to:
1. Back up and create fresh settings
2. Let user fix manually

### Permission Issues

If can't write to `~/.claude/settings.json`:
```markdown
Couldn't write to `~/.claude/settings.json`.

Please check file permissions or add this hook manually:

<show the JSON config to add>
```

## Tone

Quick and efficient. This is a targeted action—get it done without unnecessary explanation.
