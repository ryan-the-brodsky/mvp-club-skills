---
name: timeline
description: Use this skill to generate a visual timeline/history of the build from captured screenshots. Activate when users say "show build history", "timeline of progress", "what did we build?", "visual summary". Invoke with screenshot-journal:timeline.
---

# Screenshot Journal: Timeline

You are generating a visual timeline that shows the progression of the build through captured screenshots.

## Prerequisites

- Screenshots should exist in `.screenshot-journal/` directory
- Or, offer to start capturing now

## Finding Screenshots

Look for screenshots in:
```
.screenshot-journal/
├── 2024-01-14/
│   ├── 09-30-initial-setup.png
│   └── 14-00-first-component.png
├── 2024-01-15/
│   ├── 10-00-auth-flow.png
│   └── 16-30-dashboard.png
└── timeline.md
```

Also check for metadata files that describe each screenshot.

## Timeline Generation

### 1. Gather Screenshots
Collect all screenshots, sorted by date/time.

### 2. Extract Context
For each screenshot, gather:
- Timestamp
- Description (from filename or metadata)
- Related commit (if tracked)
- Page/feature shown

### 3. Generate Timeline Document

```markdown
# Build Timeline: [Project Name]

**Generated:** 2024-01-16
**Total captures:** 12
**Build duration:** 3 days

---

## Day 1: Foundation (Jan 14)

### 9:30 AM - Initial Setup
![Initial setup](./2024-01-14/09-30-initial-setup.png)
*Project scaffolded, basic layout in place*

### 2:00 PM - First Component
![First component](./2024-01-14/14-00-first-component.png)
*Header component implemented with navigation*

**Day 1 Summary:** Set up project foundation and core layout

---

## Day 2: Authentication (Jan 15)

### 10:00 AM - Auth Flow
![Auth flow](./2024-01-15/10-00-auth-flow.png)
*Login and signup forms working*

### 4:30 PM - Dashboard
![Dashboard](./2024-01-15/16-30-dashboard.png)
*Main dashboard view with user data*

**Day 2 Summary:** Implemented full authentication and main dashboard

---

## Day 3: Polish (Jan 16)

### 11:00 AM - Charts Added
![Charts](./2024-01-16/11-00-charts.png)
*Added data visualization to dashboard*

### 3:00 PM - Mobile Responsive
![Mobile view](./2024-01-16/15-00-mobile.png)
*Responsive design implemented*

**Day 3 Summary:** Added visualizations and mobile support

---

## Progress Summary

| Milestone | Status | Screenshot |
|-----------|--------|------------|
| Project setup | ✅ | Day 1, 9:30 |
| Authentication | ✅ | Day 2, 10:00 |
| Dashboard | ✅ | Day 2, 16:30 |
| Data viz | ✅ | Day 3, 11:00 |
| Mobile | ✅ | Day 3, 15:00 |

---

## Visual Progression

*First → Latest*

![](./2024-01-14/09-30-initial-setup.png) → ![](./2024-01-15/16-30-dashboard.png) → ![](./2024-01-16/15-00-mobile.png)
```

## Timeline Variants

### Compact Timeline
For quick overview:
```markdown
## Build Progress

| Date | Milestone | Preview |
|------|-----------|---------|
| Jan 14 | Initial setup | [thumb] |
| Jan 15 | Auth + Dashboard | [thumb] |
| Jan 16 | Charts + Mobile | [thumb] |
```

### Feature-Focused Timeline
Organized by feature rather than date:
```markdown
## Feature Progress

### Authentication
1. Login form (Jan 15, 10:00)
2. Signup form (Jan 15, 11:30)
3. Password reset (Jan 15, 14:00)

### Dashboard
1. Basic layout (Jan 15, 16:30)
2. Data tables (Jan 16, 09:00)
3. Charts (Jan 16, 11:00)
```

### Diff Timeline
Highlighting changes between captures:
```markdown
## Changes Over Time

### Jan 14 → Jan 15
**Added:**
- Header navigation
- Authentication forms
- User dashboard

### Jan 15 → Jan 16
**Added:**
- Data visualization
- Mobile responsive design
**Changed:**
- Dashboard layout refined
```

## When No Screenshots Exist

```markdown
No screenshots found in `.screenshot-journal/`.

Want me to:
1. Start capturing now? (`screenshot-journal:capture`)
2. Create the journal directory structure?
3. Set up auto-capture on key events?
```

## Saving the Timeline

Save generated timeline to:
```
.screenshot-journal/timeline.md
```

Or export to:
- PDF for sharing
- Markdown for documentation
- HTML for preview

## After Generation

- "Timeline generated! Want to share it with stakeholders?"
- "Should I capture the current state to add to the timeline?"
- "Want to compare any two points in the timeline?"

## Tone

Be celebratory—timelines show progress. Emphasize how far the build has come. This is documentation that should feel good to look at.
