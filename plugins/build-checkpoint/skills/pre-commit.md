---
name: pre-commit
description: This skill runs automatically before git commits (via hook) or can be invoked manually. Performs quick validation to catch obvious issues before committing code. Invoke with build-checkpoint:pre-commit.
---

# Build Checkpoint: Pre-Commit

You are running a quick validation check before a commit. The goal is to catch obvious issues without slowing down the developer.

## Trigger

This skill activates:
- Automatically via `PreToolUse` hook on `git commit`
- Manually when user says "check before I commit"

## Quick Check Process

### 1. Is the App Running?
- Check if dev server is running
- If not, warn but don't block (they might be committing non-app code)

### 2. Does It Load?
- If server is running, load the main page
- Check for errors on load
- Timeout after configured seconds (default: 30)

### 3. Basic Smoke Test
- Click main CTA if identifiable
- Verify something happens
- Check console for errors

### 4. Quick Report

```markdown
## Pre-Commit Check

**Status:** ✅ Pass / ⚠️ Warning / ❌ Fail

### Checks
- [x] App loads
- [x] No console errors
- [x] Main action works

**Ready to commit.**
```

Or if issues:

```markdown
## Pre-Commit Check

**Status:** ❌ Fail

### Issues Found
- Console error: "TypeError: Cannot read property 'map' of undefined"
- Main button click caused error

### Recommendation
Fix the error before committing, or use `build-checkpoint:skip "WIP: fixing map error"` to commit anyway with a note.
```

## Handling Different Scenarios

### Server Not Running
```markdown
**Status:** ⚠️ Warning

Dev server doesn't appear to be running. This might be fine if you're committing:
- Documentation changes
- Config files
- Non-UI code

Proceed with commit? Or start the server first?
```

### Test Timeout
```markdown
**Status:** ⚠️ Warning

Checks timed out after 30s. The app might be:
- Slow to load (performance issue?)
- Stuck in a loading state
- Requiring authentication

Proceed with commit, or investigate?
```

### Everything Passes
```markdown
**Status:** ✅ Pass

Quick check complete. App loads, main action works, no errors.

Ready to commit!
```

## Skip Handling

If the user wants to skip:

```markdown
Skipping pre-commit check.

Note: Consider adding a reason to your commit message:
`git commit -m "WIP: auth flow - pre-commit skipped"`

This helps track which commits weren't validated.
```

## Performance

This check should complete in under 30 seconds. If it's taking longer:
- Reduce to just "does it load?"
- Skip interaction testing
- Report timing for user awareness

## Tone

Be quick and helpful. This runs on every commit—don't be verbose. Pass = short confirmation. Fail = clear issue + suggestion. Don't lecture about best practices.
