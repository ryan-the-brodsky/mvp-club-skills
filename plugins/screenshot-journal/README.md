# Screenshot Journal

Visual history of your build.

## The Problem

Vibe coders make rapid progress, but it's hard to remember what the app looked like yesterday, last week, or before that "small refactor." Screenshot Journal automatically captures and organizes visual documentation of your build.

## Why Visual History Matters

- **Track progress** - See how far you've come
- **Debug regressions** - "When did that button move?"
- **Share updates** - Show stakeholders visual progress
- **Document decisions** - "We changed this because..."

## Skills

### `screenshot-journal:capture`
Take an annotated screenshot right now.
```
"Screenshot this"
"Capture the current state"
"Document what we have"
```

### `screenshot-journal:compare`
Side-by-side comparison of expectation vs reality.
```
"Compare to the mockup"
"How close are we to the design?"
"Show PRD vs actual"
```

### `screenshot-journal:timeline`
Generate a visual timeline of the entire build.
```
"Show me the build history"
"Generate a progress timeline"
"What did we build?"
```

## Automatic Captures

Screenshot Journal can auto-capture at key moments:

| Trigger | What's Captured |
|---------|-----------------|
| Server start | Initial app state |
| After milestone | Before/after comparison |
| Before commit | Current state snapshot |
| On request | Whatever you ask for |

## Storage

Screenshots are stored in:
```
.screenshot-journal/
├── 2024-01-15/
│   ├── 09-30-initial-load.png
│   ├── 10-45-after-auth-flow.png
│   └── 14-20-pre-commit.png
├── 2024-01-16/
│   └── ...
└── timeline.md
```

## Part of the Work Loop

Screenshot Journal documents the **Build** and **Evaluate** phases:

```
Articulate → Build → Prompt → Execute → Evaluate → Iterate
               ↑                           ↑
         capture progress            document results
```

## Example Timeline Output

```markdown
# Build Timeline: My App

## Day 1 - Foundation
![Initial landing page](./2024-01-15/09-30-initial-load.png)
*First working version - basic layout in place*

![After adding auth](./2024-01-15/14-20-after-auth.png)
*Login/signup forms working*

## Day 2 - Core Features
![Dashboard v1](./2024-01-16/10-00-dashboard.png)
*Main dashboard with data display*

![Dashboard with charts](./2024-01-16/16-30-dashboard-charts.png)
*Added visualization components*
```
