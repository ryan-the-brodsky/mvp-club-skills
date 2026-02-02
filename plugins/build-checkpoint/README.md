# Build Checkpoint

Progressive validation gates for vibe coders.

## The Problem

Vibe coders build fast—sometimes too fast. Code gets committed that doesn't work. PRs get opened with broken features. Build Checkpoint adds gentle gates that catch issues before they compound.

## How It Works

Checkpoints trigger at natural breakpoints in your workflow:

| Trigger | Check | Rigor Level |
|---------|-------|-------------|
| Before commit | `pre-commit` | Quick smoke test |
| Before push to main | `pre-push` | Deploy-ready validation |
| Before PR | `pre-pr` | Full user flow validation |

## Skills

### `build-checkpoint:configure`
Customize which checks run when. Enable/disable specific triggers.

### `build-checkpoint:pre-commit`
Quick validation before committing:
- Is the app still running?
- Does the main action work?
- Any obvious errors?

### `build-checkpoint:pre-push`
Deploy-ready validation before pushing to main. For vibe coders who push directly to main (no branches/PRs), this is your last line of defense:
- Full smoke test
- Screenshot current state
- Verify main user flow
- Check console for errors

### `build-checkpoint:pre-pr`
Comprehensive validation before opening a PR:
- All user flows from PRD
- Screenshot documentation
- Agent handle coverage check

### `build-checkpoint:skip`
Sometimes you need to commit work-in-progress:
```
build-checkpoint:skip "WIP: auth flow incomplete"
```
This bypasses the check but adds a note to the commit.

## Configuration

Checkpoints can be configured per-project:

```json
{
  "build-checkpoint": {
    "pre-commit": {
      "enabled": true,
      "level": "smoke"
    },
    "pre-push": {
      "enabled": true,
      "level": "deploy-ready",
      "capture-screenshot": true
    },
    "pre-pr": {
      "enabled": true,
      "level": "full",
      "require-screenshots": true
    }
  }
}
```

## Part of the Work Loop

Build Checkpoint enforces the **Evaluate** phase at key moments:

```
Articulate → Build → Prompt → Execute → Evaluate → Iterate
                                            ↑
                              checkpoints enforce this
```

## Philosophy

- **Gates, not walls** - Checkpoints should help, not block
- **Progressive rigor** - More checks for bigger changes
- **Skip with intention** - Bypassing is allowed but recorded
- **Fast feedback** - Checks should complete in seconds, not minutes
