# MVP Club Claude Skills

Vibe coding tools that turn new builders into confident AI-first practitioners.

## Quick Start

```bash
# Add the marketplace (fetches from GitHub - auto-updates on each use)
/plugin marketplace add mvp-club/mvp-club-skills

# Install a plugin
/plugin install prd-manager@mvp-club-skills
```

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

### Pre-Commit Validation

Automatically validate before committing:

```json
{
  "hooks": {
    "PreToolUse": {
      "git commit": ["build-checkpoint:pre-commit"]
    }
  }
}
```

### Pre-Push Validation (Recommended for Vibe Coders)

Validate before pushing to main. For vibe coders who push directly to main (no branches/PRs), this is your deploy gate:

```json
{
  "hooks": {
    "PreToolUse": {
      "git push": ["build-checkpoint:pre-push"]
    }
  }
}
```

### Pre-PR Validation

Full validation before opening a PR:

```json
{
  "hooks": {
    "PreToolUse": {
      "gh pr create": ["build-checkpoint:pre-pr"]
    }
  }
}
```

### Flow Questions (Coaching Prompts)

Get contextual questions while building:

```json
{
  "hooks": {
    "PostToolUse": {
      "Write": ["flow-questions:on-new-file"],
      "Edit": ["flow-questions:on-edit"]
    }
  }
}
```

### Keep PRD in Sync

```json
{
  "hooks": {
    "post_session": ["prd-manager:update"]
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

Learn more at [mvpclub.io](https://mvpclub.io)

## Contributing

Have ideas for new skills? Open an issue or PR. We're building this for the community.

## License

MIT
