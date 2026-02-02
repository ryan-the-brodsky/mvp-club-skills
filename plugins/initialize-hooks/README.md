# Initialize Hooks

One-command setup for MVP Club Skills hooks. Get validation gates and coaching prompts configured in seconds.

## Quick Start

```bash
initialize-hooks:setup
```

The setup wizard will:
1. Show you available profiles
2. Let you choose based on your workflow
3. Configure your `~/.claude/settings.json`

## Skills

| Skill | Description |
|-------|-------------|
| `setup` | Interactive wizard to configure hooks |
| `profiles` | View available profiles and hooks |
| `add-hook` | Add a single hook by ID |
| `remove-hook` | Remove a hook from your settings |

## Profiles

### Minimal
Light guardrails for experienced developers.
- Pre-push validation

### Vibe Coder
For developers who push directly to main.
- Pre-push validation
- Flow questions (coaching prompts)

### Full Suite
Comprehensive support for new builders.
- Pre-commit validation
- Pre-push validation
- Pre-PR validation
- Flow questions
- PRD sync

## Individual Hooks

Don't want a full profile? Add hooks one at a time:

```bash
initialize-hooks:add-hook pre-push
initialize-hooks:add-hook flow-questions
```

Available hook IDs:
- `pre-commit` - Validation before commits
- `pre-push` - Validation before pushing to main
- `pre-pr` - Validation before opening PRs
- `flow-questions` - Coaching prompts when editing files
- `prd-sync` - PRD updates at end of session

## Managing Hooks

```bash
# See what's configured
initialize-hooks:profiles

# Add a hook
initialize-hooks:add-hook pre-push

# Remove a hook
initialize-hooks:remove-hook flow-questions
```

## Source of Truth

All hook definitions come from `recommended-hooks.json` in the repository root. This ensures consistency across all installations.

## How Hooks Work

Hooks automatically trigger skills at key moments:

| Hook | When | What Runs |
|------|------|-----------|
| Pre-push | Before `git push` | `build-checkpoint:pre-push` |
| Pre-commit | Before `git commit` | `build-checkpoint:pre-commit` |
| Pre-PR | Before `gh pr create` | `build-checkpoint:pre-pr` |
| Flow questions | After `Write`/`Edit` | `flow-questions:on-new-file/on-edit` |
| PRD sync | End of session | `prd-manager:update` |

## Temporarily Skipping

Need to bypass validation for a quick push?

```bash
build-checkpoint:skip "Hotfix - will validate in next push"
```

## Troubleshooting

### Hooks Not Running

1. Check your settings: `cat ~/.claude/settings.json`
2. Verify the hooks section exists and has the right structure
3. Re-run setup: `initialize-hooks:setup`

### Want to Start Fresh

Remove all MVP Club hooks and reconfigure:

```bash
initialize-hooks:remove-hook pre-push
initialize-hooks:remove-hook flow-questions
# etc.

initialize-hooks:setup
```
