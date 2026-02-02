---
name: remove-hook
description: Remove a hook from your Claude Code settings. Specify the hook by ID. Invoke with initialize-hooks:remove-hook <hook-id>.
---

# Initialize Hooks: Remove Hook

You are removing a hook from the user's Claude Code settings.

## Process

### Step 1: Parse Arguments

Check if the user specified a hook ID:
- `initialize-hooks:remove-hook pre-push` → Remove pre-push hook
- `initialize-hooks:remove-hook` (no argument) → Show current hooks and ask

### Step 2: Read Current Settings

Read `~/.claude/settings.json` to see what hooks are currently configured.

If no settings file exists:
```markdown
No settings file found at `~/.claude/settings.json`.

No hooks to remove.
```

### Step 3: If No Hook ID Provided

Show currently configured hooks and ask which to remove:

```markdown
## Current Hooks

| Hook | Trigger | Status |
|------|---------|--------|
| Pre-push validation | Before `git push` | Active |
| Flow questions | After `Write`/`Edit` | Active |

Which hook would you like to remove?
```

Use AskUserQuestion with the currently active hooks as options.

### Step 4: Validate Hook Exists

If the specified hook isn't in their settings:
```markdown
The **pre-pr** hook is not in your settings.

Currently configured hooks:
- `pre-push` - Pre-Push Validation
- `flow-questions` - Flow Questions

Nothing to remove.
```

### Step 5: Confirm Removal

```markdown
## Remove: Pre-Push Validation

This will remove the pre-push validation hook from your settings.

After removal:
- `git push` will no longer trigger validation
- You can re-add it anytime with `initialize-hooks:add-hook pre-push`

Remove this hook? (yes/no)
```

### Step 6: Remove Hook

If confirmed:
1. Read current `~/.claude/settings.json`
2. Remove the hook from the appropriate section (PreToolUse, PostToolUse, or Stop)
3. Clean up empty arrays/objects if needed
4. Write the updated settings file

**Identifying hooks to remove:**

For MVP Club Skills hooks, look for these patterns:
- `build-checkpoint:pre-commit` in PreToolUse with matcher `Bash(git commit)`
- `build-checkpoint:pre-push` in PreToolUse with matcher `Bash(git push)`
- `build-checkpoint:pre-pr` in PreToolUse with matcher `Bash(gh pr create)`
- `flow-questions:on-new-file` in PostToolUse with matcher `Write`
- `flow-questions:on-edit` in PostToolUse with matcher `Edit`
- `prd-manager:update` in Stop

### Step 7: Confirm Success

```markdown
## Hook Removed

**Pre-Push Validation** has been removed from your settings.

`git push` will no longer trigger validation.

### To Re-Add
```
initialize-hooks:add-hook pre-push
```

### Other Commands
- `initialize-hooks:profiles` - See available profiles
- `initialize-hooks:setup` - Run the full setup wizard
```

## Error Handling

### Can't Parse Settings

If the settings file has invalid JSON:
```markdown
Couldn't parse `~/.claude/settings.json`. The file may contain invalid JSON.

Please check the file manually or run:
```
initialize-hooks:setup
```
to reconfigure your hooks.
```

### Non-MVP Club Hooks

If the user tries to remove a hook that isn't from MVP Club Skills:
```markdown
The hook you specified doesn't appear to be from MVP Club Skills.

This tool only manages MVP Club Skills hooks. To remove other hooks, edit `~/.claude/settings.json` directly.
```

### All Hooks Removed

If removing the last hook:
```markdown
## Hook Removed

No MVP Club Skills hooks remain in your settings.

To add hooks back:
- `initialize-hooks:setup` - Run the setup wizard
- `initialize-hooks:add-hook <hook-id>` - Add a specific hook
```

## Tone

Clear and direct. Removing something should feel safe—reassure the user they can re-add it easily.

## Important

- Only remove hooks that are part of MVP Club Skills
- Preserve all other settings and hooks
- Leave the settings file in a valid state even if removing the last hook
