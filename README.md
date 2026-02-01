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

| Plugin | Skills | Description |
|--------|--------|-------------|
| **prd-manager** | `generate`, `update`, `compare` | Complete PRD management suite |
| **work-loop-coach** | `coach` | Work Loop methodology guidance |

## Skill Invocation

Skills are invoked as `plugin-name:skill-name`:

```bash
prd-manager:generate      # Create a new PRD
prd-manager:update        # Update PRD after building
prd-manager:compare       # Compare PRD to implementation
work-loop-coach:coach     # Get methodology guidance
```

## The Work Loop

These skills support the MVP Club Work Loop methodology:

**Articulate** → **Build** → **Prompt** → **Execute** → **Evaluate** → **Iterate**

| Phase | Supported By |
|-------|--------------|
| Articulate | `prd-manager:generate` |
| Build/Prompt/Execute | `work-loop-coach:coach` |
| Evaluate | `prd-manager:compare` |
| Iterate | `prd-manager:update` |

## Post-Session Hooks

Keep your PRD in sync automatically:

```json
{
  "hooks": {
    "post_session": ["prd-manager:update"]
  }
}
```

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
