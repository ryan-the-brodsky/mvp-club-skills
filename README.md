# MVP Club Claude Skills

Vibe coding tools that turn new builders into confident AI-first practitioners.

## Quick Start

```bash
# Add the marketplace (fetches from GitHub - auto-updates on each use)
/plugin marketplace add mvp-club/mvp-club-skills

# Install a plugin
/plugin install prd-manager@mvp-club-skills
```

## Getting Started with Hooks

The fastest way to set up hooks is with the setup wizard:

```bash
initialize-hooks:setup
```

This will walk you through choosing a profile and configure your `~/.claude/settings.json` automatically.

**Profiles available:**
- **Minimal** - Just pre-push validation
- **Vibe Coder** - Pre-push + coaching prompts (recommended for most users)
- **Full Suite** - All validation gates and coaching prompts

See `recommended-hooks.json` for the complete hook definitions (source of truth).

## Available Plugins

### Planning & Methodology

| Plugin | Skills | Description |
|--------|--------|-------------|
| **prd-manager** | `generate`, `update`, `compare` | Complete PRD management suite |
| **work-loop-coach** | `coach` | Work Loop methodology guidance |

### Testing & Validation

| Plugin | Skills | Description |
|--------|--------|-------------|
| **agent-handles** | `audit`, `suggest`, `add` | Make your app AI-testable with semantic handles |
| **claude-pilot** | `walkthrough`, `smoke-test`, `report`, `record` | Claude becomes your first user (requires Playwright MCP) |
| **build-checkpoint** | `configure`, `pre-commit`, `pre-push`, `pre-pr`, `skip` | Progressive validation gates at natural breakpoints |

### Documentation & Guidance

| Plugin | Skills | Description |
|--------|--------|-------------|
| **screenshot-journal** | `capture`, `compare`, `timeline` | Visual build history with annotated screenshots |
| **flow-questions** | `on-new-file`, `on-edit`, `prompt-me`, `configure` | Hook-driven prompts at the right moments |

### Setup & Configuration

| Plugin | Skills | Description |
|--------|--------|-------------|
| **initialize-hooks** | `setup`, `profiles`, `add-hook`, `remove-hook` | One-command setup for hooks |

## Skill Invocation

Skills are invoked as `plugin-name:skill-name`:

```bash
# Planning
prd-manager:generate      # Create a new PRD
prd-manager:update        # Update PRD after building
prd-manager:compare       # Compare PRD to implementation
work-loop-coach:coach     # Get methodology guidance

# Testing
agent-handles:audit       # Find missing handles in your codebase
agent-handles:add         # Add handles to components
claude-pilot:smoke-test   # Quick sanity check
claude-pilot:walkthrough  # Full user flow test with screenshots
claude-pilot:report       # Generate a First User Report

# Documentation
screenshot-journal:capture   # Take annotated screenshot
screenshot-journal:timeline  # Generate visual build history
flow-questions:prompt-me     # Get validation questions
```

## The Work Loop

These skills support the MVP Club Work Loop methodology:

**Articulate** → **Build** → **Prompt** → **Execute** → **Evaluate** → **Iterate**

| Phase | Supported By |
|-------|--------------|
| Articulate | `prd-manager:generate` |
| Build | `work-loop-coach:coach`, `flow-questions`, `agent-handles:add` |
| Evaluate | `claude-pilot`, `prd-manager:compare`, `screenshot-journal` |
| Iterate | `prd-manager:update`, `build-checkpoint` |

## Hooks

**Recommended:** Use `initialize-hooks:setup` to configure hooks automatically. The wizard will set up your `~/.claude/settings.json` based on your workflow.

All hook definitions are in `recommended-hooks.json` (source of truth).

### Available Hooks

| Hook | Trigger | Description |
|------|---------|-------------|
| Pre-commit | Before `git commit` | Quick validation before commits |
| Pre-push | Before `git push` | Thorough validation before pushing to main |
| Pre-PR | Before `gh pr create` | Full validation before pull requests |
| Flow questions | After `Write`/`Edit` | Coaching prompts about validation and UX |
| PRD sync | End of session | Updates PRD with session changes |

### Manual Hook Configuration

If you prefer to configure hooks manually, here are the JSON configs:

#### Pre-Commit Validation

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash(git commit)",
        "hooks": [{ "type": "skill", "skill": "build-checkpoint:pre-commit" }]
      }
    ]
  }
}
```

#### Pre-Push Validation (Recommended for Vibe Coders)

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash(git push)",
        "hooks": [{ "type": "skill", "skill": "build-checkpoint:pre-push" }]
      }
    ]
  }
}
```

#### Pre-PR Validation

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash(gh pr create)",
        "hooks": [{ "type": "skill", "skill": "build-checkpoint:pre-pr" }]
      }
    ]
  }
}
```

#### Flow Questions (Coaching Prompts)

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write",
        "hooks": [{ "type": "skill", "skill": "flow-questions:on-new-file" }]
      },
      {
        "matcher": "Edit",
        "hooks": [{ "type": "skill", "skill": "flow-questions:on-edit" }]
      }
    ]
  }
}
```

#### PRD Sync

```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [{ "type": "skill", "skill": "prd-manager:update" }]
      }
    ]
  }
}
```

## MCP Requirements

Some plugins require MCPs to be installed:

| Plugin | Required MCP |
|--------|--------------|
| **claude-pilot** | Playwright |
| **screenshot-journal** | Playwright |

iOS Simulator MCP is optional for mobile app testing.

## Updates

**GitHub-hosted marketplaces auto-update.** When you add a marketplace from a GitHub repo, Claude Code fetches the latest version each time you use it. No manual update needed.

To check for new plugins or skills:
```bash
/plugin marketplace list mvp-club-skills
```

## Philosophy

- **Practice over training** - Skills are learned through doing, not reading
- **Human + AI Teams** - You drive goals and judgment; AI accelerates execution
- **Confidence through competence** - Real capability comes from shipping real things

## About MVP Club

MVP Club Consulting helps organizations develop AI-first mindsets and capabilities. We believe the fundamental unit of labor is shifting from the individual to the Human + AI Team.

Learn more at [mvpclub.ai](https://mvpclub.ai)

## Contributing

Have ideas for new skills? Open an issue or PR. We're building this for the community.

## License

MIT
