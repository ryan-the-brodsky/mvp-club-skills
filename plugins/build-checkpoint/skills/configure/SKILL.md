---
name: configure
description: Use this skill to set up or modify build checkpoint configuration. Activate when users say "configure checkpoints", "set up build gates", "change checkpoint settings", "disable pre-commit checks". Invoke with build-checkpoint:configure.
---

# Build Checkpoint Configuration

You are helping a user configure their build checkpoint settings—which validation checks run at which triggers.

## Default Configuration

If no configuration exists, these are the defaults:

```json
{
  "build-checkpoint": {
    "pre-commit": {
      "enabled": true,
      "level": "smoke",
      "timeout": 30
    },
    "pre-pr": {
      "enabled": true,
      "level": "full",
      "require-screenshots": true,
      "timeout": 120
    }
  }
}
```

## Configuration Options

### `pre-commit`

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `enabled` | boolean | `true` | Run checks before commits |
| `level` | string | `"smoke"` | `"smoke"` or `"full"` |
| `timeout` | number | `30` | Max seconds to wait |
| `skip-on-wip` | boolean | `false` | Auto-skip if commit message contains "WIP" |

### `pre-pr`

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `enabled` | boolean | `true` | Run checks before PRs |
| `level` | string | `"full"` | `"smoke"` or `"full"` |
| `require-screenshots` | boolean | `true` | Include screenshots in validation |
| `timeout` | number | `120` | Max seconds to wait |
| `flows` | array | `[]` | Specific flows to test (empty = all from PRD) |

### Validation Levels

**Smoke level:**
- App loads
- Main action works
- No console errors

**Full level:**
- All user flows from PRD
- Agent handle coverage check
- Screenshot at each step
- Error state testing

## Configuration Process

1. **Ask what they want to change:**
   - "What checkpoint behavior would you like to modify?"
   - "Are checks too slow? Too intrusive? Not catching enough?"

2. **Understand their workflow:**
   - "Do you commit frequently with small changes?"
   - "Do you use WIP commits?"
   - "How thorough should PR checks be?"

3. **Propose configuration:**
   ```json
   {
     "build-checkpoint": {
       "pre-commit": {
         "enabled": true,
         "level": "smoke",
         "skip-on-wip": true
       }
     }
   }
   ```

4. **Explain trade-offs:**
   - Faster checks = less coverage
   - Disabled checks = risk of broken commits
   - WIP skip = convenient but requires discipline

## Common Configurations

### "I commit constantly, checks are annoying"
```json
{
  "pre-commit": {
    "enabled": true,
    "level": "smoke",
    "skip-on-wip": true,
    "timeout": 15
  }
}
```

### "I want thorough checks everywhere"
```json
{
  "pre-commit": {
    "enabled": true,
    "level": "full",
    "timeout": 60
  },
  "pre-pr": {
    "enabled": true,
    "level": "full",
    "require-screenshots": true
  }
}
```

### "Just check PRs, not commits"
```json
{
  "pre-commit": {
    "enabled": false
  },
  "pre-pr": {
    "enabled": true,
    "level": "full"
  }
}
```

## Where Configuration Lives

Configuration should be stored in one of:
- `.claude/build-checkpoint.json` (preferred)
- `claude.config.json` under `build-checkpoint` key
- Project's `package.json` under `claude.build-checkpoint`

## Tone

Be helpful and non-judgmental. Some developers want lots of checks, some want minimal interruption. Both are valid. Help them find the right balance for their workflow.
