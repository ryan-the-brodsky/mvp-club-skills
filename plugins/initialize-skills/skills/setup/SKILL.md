---
name: setup
description: Interactive wizard to install MVP Club Skills plugins and configure hooks. The main onboarding entry point. Invoke with initialize-skills:setup.
---

# Initialize Skills: Setup Wizard

You are running the MVP Club Skills setup wizard. This is the main onboarding flow that helps users get set up with the right plugins and hooks for their workflow.

## Overview

This wizard will:
1. Understand the user's workflow and experience level
2. Recommend or let them choose plugins
3. Install the selected plugins
4. Configure hooks in their settings
5. Provide a summary and next steps

## Setup Process

### Step 1: Welcome

```markdown
## Welcome to MVP Club Skills!

I'll help you get set up with the right tools for your workflow. This will only take a minute.

First, let me understand how you work...
```

### Step 2: Understand Their Workflow

Use AskUserQuestion to understand their workflow:

**Question 1: Experience Level**
```
How would you describe your experience with AI-assisted coding?

1. **New to vibe coding** - I'm just getting started and want guidance
2. **Some experience** - I've built a few things but want better workflows
3. **Experienced** - I know what I'm doing, just want the tools
```

**Question 2: Git Workflow**
```
How do you typically work with git?

1. **Push to main** - I push directly to main (vibe coder style)
2. **Branches + PRs** - I use feature branches and pull requests
3. **Not sure yet** - I'm still figuring out my workflow
```

### Step 3: Present Presets Based on Answers

Based on their answers, recommend a preset:

#### For "New to vibe coding" + any git workflow:
```markdown
## Recommended: Full Suite

Since you're getting started, I recommend the full suite of tools:

### Plugins to Install
| Plugin | What it does |
|--------|--------------|
| **prd-manager** | Helps you plan what you're building |
| **work-loop-coach** | Guides you through the build process |
| **agent-handles** | Makes your app testable by AI |
| **claude-pilot** | Tests your app like a real user |
| **build-checkpoint** | Validates before commits/pushes |
| **screenshot-journal** | Captures visual progress |
| **flow-questions** | Asks helpful questions as you build |

### Hooks to Configure
- Pre-push validation (checks before pushing to main)
- Flow questions (coaching prompts when editing files)
- PRD sync (keeps your PRD updated)

This gives you comprehensive support while you're learning.

Sound good? (yes / let me customize)
```

#### For "Some experience" + "Push to main":
```markdown
## Recommended: Vibe Coder

You've got some experience and push directly to main. Here's what I recommend:

### Plugins to Install
| Plugin | What it does |
|--------|--------------|
| **prd-manager** | Keep track of what you're building |
| **build-checkpoint** | Validates before you push to production |
| **flow-questions** | Occasional helpful prompts |
| **claude-pilot** | Quick smoke tests when needed |

### Hooks to Configure
- Pre-push validation (your deploy gate)
- Flow questions (light coaching prompts)

This keeps you moving fast with a safety net.

Sound good? (yes / let me customize)
```

#### For "Some experience" + "Branches + PRs":
```markdown
## Recommended: PR Workflow

You use branches and PRs. Here's what I recommend:

### Plugins to Install
| Plugin | What it does |
|--------|--------------|
| **prd-manager** | Keep track of what you're building |
| **build-checkpoint** | Validates before commits and PRs |
| **agent-handles** | Makes your app testable |
| **claude-pilot** | Tests before you open a PR |

### Hooks to Configure
- Pre-commit validation (quick checks)
- Pre-PR validation (thorough checks before PR)

This ensures quality at each stage of your workflow.

Sound good? (yes / let me customize)
```

#### For "Experienced":
```markdown
## Recommended: Minimal + Pick Your Own

You know what you're doing. Here's the minimal setup:

### Plugins to Install
| Plugin | What it does |
|--------|--------------|
| **build-checkpoint** | Validation gates when you need them |

### Hooks to Configure
- Pre-push validation (optional safety net)

Want to add more plugins? Here's what's available:

| Plugin | Purpose |
|--------|---------|
| **prd-manager** | PRD management |
| **work-loop-coach** | Methodology guidance |
| **agent-handles** | AI-testable handles |
| **claude-pilot** | Automated user testing |
| **screenshot-journal** | Visual documentation |
| **flow-questions** | Coaching prompts |

Which additional plugins would you like? (or "none" for minimal)
```

### Step 4: Customize (If Requested)

If user wants to customize, show all available plugins:

```markdown
## Available Plugins

Select which plugins you want to install:

### Planning & Methodology
- [ ] **prd-manager** - Generate, update, and compare PRDs
- [ ] **work-loop-coach** - Work Loop methodology guidance

### Testing & Validation
- [ ] **agent-handles** - Add AI-testable handles to your app
- [ ] **claude-pilot** - Automated user testing (requires Playwright MCP)
- [ ] **build-checkpoint** - Validation gates for git operations

### Documentation & Guidance
- [ ] **screenshot-journal** - Visual build history (requires Playwright MCP)
- [ ] **flow-questions** - Coaching prompts while building

Which plugins would you like?
```

Use AskUserQuestion with multiSelect to let them choose multiple plugins.

### Step 5: Confirm Before Installing

Show exactly what will happen:

```markdown
## Ready to Install

Here's what I'll do:

### Plugins to Install
1. `/plugin install prd-manager@mvp-club-skills`
2. `/plugin install build-checkpoint@mvp-club-skills`
3. `/plugin install flow-questions@mvp-club-skills`

### Hooks to Configure
Will add to `~/.claude/settings.json`:
- Pre-push validation (before `git push`)
- Flow questions (after `Write`/`Edit`)

Proceed? (yes/no)
```

### Step 6: Execute Installation

If confirmed, execute the plugin install commands:

```bash
/plugin install prd-manager@mvp-club-skills
/plugin install build-checkpoint@mvp-club-skills
/plugin install flow-questions@mvp-club-skills
# ... etc for each selected plugin
```

**Important:** Execute these as actual commands. The user needs to see the installation happen.

Report progress as you go:
```markdown
Installing plugins...

- [x] prd-manager installed
- [x] build-checkpoint installed
- [x] flow-questions installed

All plugins installed!
```

### Step 7: Configure Hooks

After plugins are installed, configure hooks:

1. Read `recommended-hooks.json` from the mvp-club-skills repository
2. Read current `~/.claude/settings.json` (or create if doesn't exist)
3. Merge the appropriate hooks based on their selections
4. Write the updated settings file

```markdown
Configuring hooks...

- [x] Pre-push validation configured
- [x] Flow questions configured

Hooks configured!
```

### Step 8: Success Summary

```markdown
## You're All Set!

### Installed Plugins
- **prd-manager** - `prd-manager:generate`, `prd-manager:update`, `prd-manager:compare`
- **build-checkpoint** - Runs automatically before pushes
- **flow-questions** - Runs automatically when editing files

### Active Hooks
- **Pre-push** - Validates before pushing to main
- **Flow questions** - Coaching prompts when creating/editing files

### Try These Commands
```bash
prd-manager:generate    # Start planning your build
work-loop-coach:coach   # Get methodology guidance
claude-pilot:smoke-test # Test your app
```

### Need Help?
- `initialize-hooks:profiles` - View/change hook profiles
- `initialize-hooks:add-hook` - Add more hooks
- `initialize-hooks:remove-hook` - Remove a hook

Happy building!
```

## Plugin Installation Commands

For reference, here are all the install commands:

| Plugin | Command |
|--------|---------|
| prd-manager | `/plugin install prd-manager@mvp-club-skills` |
| work-loop-coach | `/plugin install work-loop-coach@mvp-club-skills` |
| agent-handles | `/plugin install agent-handles@mvp-club-skills` |
| claude-pilot | `/plugin install claude-pilot@mvp-club-skills` |
| build-checkpoint | `/plugin install build-checkpoint@mvp-club-skills` |
| screenshot-journal | `/plugin install screenshot-journal@mvp-club-skills` |
| flow-questions | `/plugin install flow-questions@mvp-club-skills` |
| initialize-hooks | `/plugin install initialize-hooks@mvp-club-skills` |

## Handling Errors

### Plugin Already Installed
If a plugin is already installed, note it and continue:
```markdown
- [x] prd-manager (already installed)
- [x] build-checkpoint installed
```

### Installation Fails
If installation fails:
```markdown
- [x] prd-manager installed
- [ ] claude-pilot failed - requires Playwright MCP

Some plugins require additional setup. See the README for MCP requirements.
```

### Settings File Issues
If can't write to settings:
```markdown
Couldn't write to `~/.claude/settings.json`.

Your plugins are installed! To manually configure hooks, add this to your settings:

<show JSON config>
```

## Tone

Friendly and efficient. This is the user's first experience with MVP Club Skills—make it smooth and welcoming. Don't overwhelm with information; guide them step by step.

## Important Notes

- Always execute the actual `/plugin install` commands—don't just describe them
- Install `initialize-hooks` automatically so they can manage hooks later
- Read hook configs from `recommended-hooks.json` (source of truth)
- Preserve existing settings when adding hooks
- If they already have some plugins installed, acknowledge and skip those
