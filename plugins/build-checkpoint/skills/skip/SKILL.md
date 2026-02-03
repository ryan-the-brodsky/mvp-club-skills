---
name: skip
description: Use this skill to temporarily bypass a build checkpoint with a documented reason. Activate when users say "skip the check", "bypass checkpoint", "commit anyway", "I know it's broken". Invoke with build-checkpoint:skip.
---

# Build Checkpoint: Skip

You are helping a user bypass a build checkpoint intentionally. Skipping is allowed but should be documented.

## When Skipping is Appropriate

- **WIP commits** - Work in progress that's intentionally incomplete
- **Documentation only** - Changes that don't affect the app
- **Config changes** - Non-functional changes
- **Emergency fixes** - When speed matters more than process
- **Known issues** - When the issue is tracked and will be fixed later

## Skip Process

### 1. Acknowledge the Skip
```markdown
Understood. Skipping [pre-commit/pre-pr] checkpoint.
```

### 2. Ask for Reason (if not provided)
```markdown
What's the reason for skipping? This will be documented.
Examples:
- "WIP: auth flow incomplete"
- "Docs only: updated README"
- "Emergency: hotfix for prod issue #123"
```

### 3. Document the Skip

For commits, suggest including in commit message:
```markdown
Suggested commit message format:

git commit -m "Your message

[checkpoint-skipped: WIP - auth flow incomplete]"
```

For PRs, suggest including in description:
```markdown
Suggested PR description addition:

---
⚠️ **Note:** Pre-PR validation was skipped.
**Reason:** Emergency hotfix for production issue
**Tracking:** Will add tests in follow-up PR #XXX
---
```

### 4. Proceed
```markdown
Checkpoint skipped. Proceeding with [commit/PR].

Remember to:
- [ ] Address the skipped validation before merging to main
- [ ] Run full validation when the WIP is complete
```

## Skip Tracking

If the project uses a skip log, append to it:

```markdown
## Checkpoint Skip Log

| Date | Type | Reason | Resolved |
|------|------|--------|----------|
| 2024-01-15 | pre-commit | WIP: auth flow | ✅ |
| 2024-01-16 | pre-pr | Emergency hotfix | ✅ |
| 2024-01-17 | pre-commit | Docs only | N/A |
```

## Preventing Skip Abuse

If you notice frequent skips:
```markdown
I notice checkpoints have been skipped 5 times this week.

This might indicate:
- Checks are too slow → Consider `build-checkpoint:configure` to adjust
- Checks are too strict → We can tune the validation level
- Workflow mismatch → Maybe different triggers would work better

Want to discuss adjusting the checkpoint configuration?
```

## Emergency Skip

For true emergencies (production down, etc.):
```markdown
🚨 Emergency skip acknowledged.

Skipping all validation. Proceeding immediately.

After the emergency:
- [ ] Run full validation
- [ ] Document what was shipped without checks
- [ ] Consider if this revealed a gap in the process
```

## Tone

Be non-judgmental. Skipping is a legitimate workflow choice. Document it, remind them to follow up, but don't lecture. Trust that developers have reasons for their decisions.
