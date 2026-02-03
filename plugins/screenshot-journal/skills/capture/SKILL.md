---
name: capture
description: Use this skill to take an annotated screenshot of the app's current state. Activate when users say "screenshot this", "capture the app", "document current state", "take a picture of this". Invoke with screenshot-journal:capture.
---

# Screenshot Journal: Capture

You are capturing an annotated screenshot of the app's current state using Playwright.

## Prerequisites

- Playwright MCP required
- App should be running (ask for URL if not clear)

## Capture Process

### 1. Prepare
- Navigate to the requested page/state
- Wait for content to load
- Clear any transient UI (tooltips, notifications)

### 2. Capture
Take screenshot with appropriate settings:
```javascript
await page.screenshot({
  path: screenshotPath,
  fullPage: false  // Viewport only, unless full page requested
});
```

### 3. Annotate
Add metadata to the capture:
```markdown
## Screenshot Captured

**File:** `.screenshot-journal/2024-01-15/14-30-dashboard.png`
**Page:** /dashboard
**Timestamp:** 2024-01-15 14:30:22
**Note:** [User's description or auto-generated]

![Dashboard](path/to/screenshot.png)
```

### 4. Store
Save to the journal directory structure:
```
.screenshot-journal/
└── YYYY-MM-DD/
    └── HH-MM-description.png
```

## Naming Convention

Format: `HH-MM-description.png`

Examples:
- `09-30-initial-load.png`
- `14-45-after-signup-flow.png`
- `16-00-dashboard-with-data.png`
- `17-30-pre-commit-state.png`

## Asking for Context

If the user just says "screenshot this", ask:
- "What should I call this screenshot?" or auto-generate from URL
- "Any specific area to focus on, or full viewport?"
- "Is the app in the state you want to capture?"

## Screenshot Options

### Viewport (default)
Just what's visible in the browser window.

### Full Page
Entire scrollable page:
```
"Capture the full page"
"Screenshot everything, not just viewport"
```

### Element
Specific component:
```
"Screenshot just the sidebar"
"Capture the form"
```

### Multiple States
Capture a sequence:
```
"Screenshot before and after I click submit"
```

## Annotation Format

When saving to the journal, include metadata:

```markdown
---
timestamp: 2024-01-15T14:30:22Z
url: http://localhost:3000/dashboard
description: Dashboard after implementing charts
trigger: manual
related_commit: abc123
---
```

## Output

After capturing:

```markdown
## Screenshot Captured ✓

**Saved:** `.screenshot-journal/2024-01-15/14-30-dashboard-with-charts.png`

![Dashboard with charts](path/to/screenshot.png)

**Context:**
- Page: /dashboard
- Time: 2:30 PM
- Note: Dashboard after implementing charts

Want to:
- Capture another state?
- Compare to a previous screenshot?
- Add this to the timeline?
```

## If Capture Fails

```markdown
## Capture Failed

**Issue:** Could not load page - connection refused
**URL:** http://localhost:3000

Is the dev server running? Try:
- `npm run dev`
- Then retry `screenshot-journal:capture`
```

## Tone

Be efficient. Screenshots are quick documentation—capture, confirm, move on. Don't over-explain unless something goes wrong.
