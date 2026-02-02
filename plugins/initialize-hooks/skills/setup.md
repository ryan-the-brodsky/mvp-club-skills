---
name: setup
description: Interactive wizard to set up MVP Club Skills hooks. Presents profiles, shows what will be added, and modifies ~/.claude/settings.json. Invoke with initialize-hooks:setup.
---

# Initialize Hooks: Setup Wizard

You are running the hook setup wizard. This helps users configure MVP Club Skills hooks in their Claude Code settings.

## Setup Process

### Step 1: Read Hook Definitions

First, read the hook definitions from the source of truth:

```
Read: recommended-hooks.json (from the mvp-club-skills repository root)
```

This file contains all profile definitions and hook configurations.

### Step 2: Check Current Settings

Read the user's current Claude settings:

```
Read: ~/.claude/settings.json
```

Note which hooks are already configured (if any).

### Step 3: Present Profiles

Show the user the available profiles with clear descriptions:

```markdown
## Hook Profiles

Choose a profile that matches your workflow:

### 1. Minimal
Light guardrails for experienced developers. Just the essentials.

**Includes:**
- Pre-push validation (your deploy gate)

### 2. Vibe Coder (Recommended for most users)
For developers who push directly to main. Validation before deploy plus helpful coaching prompts.

**Includes:**
- Pre-push validation
- Flow questions (coaching prompts when creating/editing files)

### 3. Full Suite
Comprehensive support for new builders. All validation gates and coaching prompts enabled.

**Includes:**
- Pre-commit validation
- Pre-push validation
- Pre-PR validation
- Flow questions
- PRD sync (updates PRD at end of session)

Which profile would you like? (1, 2, or 3)
```

### Step 4: Get User Selection

Use AskUserQuestion tool to get the user's profile choice:

- Options: Minimal, Vibe Coder, Full Suite
- Allow them to say "none" or "cancel" to exit

### Step 5: Show What Will Be Added

Before making changes, show exactly what hooks will be added:

```markdown
## Hooks to Add

You selected **Vibe Coder**. Here's what will be added to your settings:

### Pre-Push Validation
- **Trigger:** Before `git push`
- **Action:** Runs `build-checkpoint:pre-push`
- **Purpose:** Validates your code before pushing to main

### Flow Questions
- **Trigger:** After `Write` or `Edit` tools
- **Action:** Runs coaching prompts
- **Purpose:** Asks helpful questions about validation and UX

These hooks will be added to `~/.claude/settings.json`.

Proceed with setup? (yes/no)
```

### Step 6: Confirm Before Modifying

Use AskUserQuestion to confirm:
- Show the exact hooks that will be added
- Explain they can remove hooks later with `initialize-hooks:remove-hook`
- Require explicit "yes" to proceed

### Step 7: Modify Settings

If confirmed, update `~/.claude/settings.json`:

1. Read the current file (or create structure if it doesn't exist)
2. Merge the new hooks into the existing hooks structure
3. Preserve any existing hooks that don't conflict
4. Write the updated file

**Important:** Use the exact hook config from `recommended-hooks.json`. The config structure should be:

```json
{
  "hooks": {
    "PreToolUse": [...],
    "PostToolUse": [...],
    "Stop": [...]
  }
}
```

### Step 8: Confirm Success

After successful update:

```markdown
## Setup Complete

Your hooks are now configured:

- [x] Pre-push validation
- [x] Flow questions

### What Happens Next

- **Pre-push:** When you run `git push`, validation will run automatically
- **Flow questions:** After creating/editing files, you'll see coaching prompts

### Useful Commands

- `initialize-hooks:profiles` - View all available profiles
- `initialize-hooks:add-hook` - Add additional hooks
- `initialize-hooks:remove-hook` - Remove a hook
- `build-checkpoint:skip` - Temporarily skip a checkpoint

Happy building!
```

## Error Handling

### Settings File Doesn't Exist

If `~/.claude/settings.json` doesn't exist:
1. Create the directory if needed: `mkdir -p ~/.claude`
2. Create a new settings file with just the hooks

### Invalid JSON

If the settings file contains invalid JSON:
1. Show the error
2. Offer to back up the file and create a fresh one
3. Or let the user fix it manually

### Existing Hooks

If hooks already exist:
1. Show what's currently configured
2. Explain new hooks will be merged
3. Warn if any hooks will be overwritten

## Tone

Be helpful and clear. This is likely the user's first interaction with hooks—make it easy to understand what they're getting. Avoid jargon; explain things in plain terms.

## Important

- Always use the hook configs from `recommended-hooks.json` exactly
- Never modify hooks that aren't part of MVP Club Skills
- Preserve the user's existing settings structure
