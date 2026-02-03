---
name: pre-push
description: This skill runs automatically before git push to main/master (via hook) or can be invoked manually. Performs validation before code goes live. More thorough than pre-commit since pushing to main often means deploying. Invoke with build-checkpoint:pre-push.
---

# Build Checkpoint: Pre-Push

You are running validation before a push to main. For vibe coders who push directly to main, this is the last line of defense before code goes live.

## Trigger

This skill activates:
- Automatically via `PreToolUse` hook on `git push` (when targeting main/master)
- Manually when user says "check before I push"

## Why Pre-Push Matters

Many vibe coders push straight to main:
- No branches, no PRs
- Push = deploy (often via Vercel, Netlify, etc.)
- This is the validation gate

## Pre-Push Check Process

### 1. Confirm Target Branch

```markdown
Pushing to **main**. Running pre-push validation...
```

If pushing to a feature branch, skip or run lighter checks:
```markdown
Pushing to feature branch `fix-auth`. Skipping full validation.
(Use `build-checkpoint:pre-push` manually for full check)
```

### 2. Is the App Running?

- Check if dev server is running
- If not running, offer to start it (this is pre-push, worth the effort)

### 3. Full Smoke Test

More thorough than pre-commit:

| Check | Description |
|-------|-------------|
| App loads | Main page renders without errors |
| Console clean | No errors or warnings in console |
| Main flow works | Primary user action completes |
| Navigation | Can navigate to key pages |
| Forms submit | If forms exist, they don't error on submit |

### 4. Screenshot Current State

Capture a screenshot of the main page:
```markdown
📸 Captured current state before push
```

This gives a reference point if something breaks after deploy.

### 5. Report

**Pass:**
```markdown
## Pre-Push Validation ✅

Pushing to **main**

### Checks Passed
- [x] App loads (1.2s)
- [x] No console errors
- [x] Main user flow works
- [x] Navigation functional

📸 Screenshot saved

**Ready to push.** This will likely deploy to production.
```

**Fail:**
```markdown
## Pre-Push Validation ❌

Pushing to **main**

### Issues Found
- ❌ Console error: "Uncaught TypeError at Dashboard.jsx:45"
- ⚠️ Form submission shows loading but never completes

### Recommendation
Fix these issues before pushing to main. This will deploy to production.

Options:
1. Fix the issues now
2. `build-checkpoint:skip "Hotfix needed - will fix in next push"`
3. Push to a branch instead: `git push origin HEAD:fix-dashboard`
```

**Warning:**
```markdown
## Pre-Push Validation ⚠️

Pushing to **main**

### Checks
- [x] App loads
- [x] No console errors
- ⚠️ Could not test main flow (no agent-handles found)

### Note
Consider adding agent-handles for better automated testing.
See: `agent-handles:add`

**Proceed with push?** The app loads, but full flow wasn't validated.
```

## Branch Detection

Detect the target branch from the git command:
- `git push` → check default push behavior
- `git push origin main` → explicitly main
- `git push -u origin main` → explicitly main
- `git push origin feature-x` → feature branch (lighter check)

## If Push is to Feature Branch

```markdown
Pushing to **feature-x** (not main).

Running quick check only:
- [x] App loads
- [x] No console errors

Full validation will run when you push to main.
```

## Handling "I need to push now"

If user insists:
```markdown
Understood. Skipping validation for this push.

⚠️ Remember: Pushing to main often means deploying to production.

If something breaks, you can:
- Revert: `git revert HEAD && git push`
- Check deploy status in your hosting dashboard
```

## Integration with Other Skills

After successful push:
```markdown
Push complete!

Suggestions:
- `screenshot-journal:capture` - Document the deployed state
- `claude-pilot:smoke-test` - Verify the live site works
```

## Performance Target

Complete within 60 seconds. If slower:
- Warn about timing
- Offer to run async and notify when done

## Tone

This is the last gate before production. Be clear about stakes without being scary. Vibe coders chose to push to main—respect that choice while helping them avoid obvious mistakes.
