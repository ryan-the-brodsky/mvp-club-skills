---
name: profiles
description: View available hook profiles and their included hooks. Read-only view of what you can configure. Invoke with initialize-hooks:profiles.
---

# Initialize Hooks: View Profiles

You are showing the user the available hook profiles. This is a read-only view to help them understand their options.

## Process

### Step 1: Read Hook Definitions

Read the hook definitions from the source of truth:

```
Read: recommended-hooks.json (from the mvp-club-skills repository root)
```

### Step 2: Display Profiles

Present all profiles with their included hooks:

```markdown
## Available Hook Profiles

### Minimal
*Light guardrails for experienced developers*

| Hook | Trigger | Description |
|------|---------|-------------|
| Pre-push validation | Before `git push` | Validates code before pushing to main |

Best for: Developers who want minimal interruption but still want a safety net before deploying.

---

### Vibe Coder
*For developers who push directly to main*

| Hook | Trigger | Description |
|------|---------|-------------|
| Pre-push validation | Before `git push` | Validates code before pushing to main |
| Flow questions | After `Write`/`Edit` | Coaching prompts about validation and UX |

Best for: Vibe coders who push directly to main and want helpful guidance without heavy process.

---

### Full Suite
*Comprehensive support for new builders*

| Hook | Trigger | Description |
|------|---------|-------------|
| Pre-commit validation | Before `git commit` | Quick checks before each commit |
| Pre-push validation | Before `git push` | Validates code before pushing to main |
| Pre-PR validation | Before `gh pr create` | Full validation before opening a PR |
| Flow questions | After `Write`/`Edit` | Coaching prompts about validation and UX |
| PRD sync | End of session | Updates your PRD with session changes |

Best for: New builders who want comprehensive guardrails and guidance throughout their workflow.

---

## Individual Hooks

You can also add hooks individually:

| Hook ID | Name | Trigger |
|---------|------|---------|
| `pre-commit` | Pre-Commit Validation | Before `git commit` |
| `pre-push` | Pre-Push Validation | Before `git push` |
| `pre-pr` | Pre-PR Validation | Before `gh pr create` |
| `flow-questions` | Flow Questions | After `Write`/`Edit` |
| `prd-sync` | PRD Sync | End of session |

## Next Steps

- `initialize-hooks:setup` - Run the setup wizard
- `initialize-hooks:add-hook <hook-id>` - Add a specific hook
```

## Tone

Informative and helpful. Help the user understand what each profile offers so they can make an informed choice.

## Important

- This is read-only - don't modify any settings
- Always read from `recommended-hooks.json` for the latest definitions
- Present information clearly with tables for easy scanning
