---
description: Use this skill to generate a comprehensive First User Report with screenshots, findings, and recommendations. Activate when users say "give me a user report", "what did you find?", "summarize the testing", "first user report". Invoke with claude-pilot:report.
---

# Claude Pilot: First User Report

You are generating a comprehensive report of your experience using an app as its first user. This combines findings from smoke tests, walkthroughs, and general exploration into an actionable document.

## Prerequisites

- Should have run at least one `smoke-test` or `walkthrough` first
- Or, start fresh and do exploration now to generate the report
- Playwright MCP required

## Before Testing: Load Agent Handles

If starting fresh or re-testing, check if an `AGENT-HANDLES.md` file exists in the project root. If it does, read it first. This file contains a complete map of all `agent-handle` selectors — use it as your reference for targeting elements reliably.

## Screenshot Directory

If starting fresh and taking new screenshots, create a new directory for this run:

```
screenshots/report-YYYY-MM-DD-HH-MM/
```

If compiling from previous test runs, reference the screenshots in their existing `screenshots/` subdirectories (e.g., `screenshots/smoke-test-2024-01-15-14-30/`, `screenshots/walkthrough-2024-01-15-16-00/`).

Create the `screenshots/` directory if it doesn't already exist. Never reuse a previous run's folder — every invocation gets a fresh timestamped directory.

## Report Structure

Generate a report following this template:

```markdown
# First User Report: [App Name]

**Tested by:** Claude Pilot
**Date:** [Date]
**URL:** [App URL]
**Time spent:** [Duration]

---

## Executive Summary

[2-3 sentences: Does the app work? What's the overall impression? Major issues?]

**Overall Status:** ✅ Ready for users / ⚠️ Needs work / ❌ Critical issues

---

## Screenshots Gallery

### Initial State
[Screenshot of landing/home page]

### Key Screens
[Screenshots of main screens encountered]

### Issues Found
[Screenshots showing problems]

---

## What Works Well

### [Category 1, e.g., "Onboarding"]
- [Specific thing that works well]
- [Why it's good from a user perspective]

### [Category 2, e.g., "Core Functionality"]
- [Specific thing that works well]
- [Why it's good]

---

## Issues Found

### Critical (Blocks Usage)
| Issue | Location | Screenshot | Impact |
|-------|----------|------------|--------|
| [Description] | [Where] | [Link] | [What it prevents] |

### Major (Degrades Experience)
| Issue | Location | Screenshot | Suggestion |
|-------|----------|------------|------------|
| [Description] | [Where] | [Link] | [How to fix] |

### Minor (Polish)
| Issue | Location | Suggestion |
|-------|----------|------------|
| [Description] | [Where] | [How to fix] |

---

## User Flows Tested

### [Flow 1 Name]
**Status:** ✅ Pass / ❌ Fail
**Steps completed:** X/Y

| Step | Action | Result | Notes |
|------|--------|--------|-------|
| 1 | [Action] | ✅/❌ | [Notes] |
| 2 | [Action] | ✅/❌ | [Notes] |

### [Flow 2 Name]
[Same format]

---

## Agent Handle Coverage

**Status:** [Good / Partial / Missing]

- Interactive elements found: X
- Elements with handles: Y
- Coverage: Z%

[If low coverage]: Recommend running `agent-handles:audit` and `agent-handles:add`

---

## Recommendations

### Immediate (Before Launch)
1. [Most critical fix]
2. [Second critical fix]

### Soon (First Update)
1. [Important improvement]
2. [Important improvement]

### Later (Nice to Have)
1. [Polish item]
2. [Polish item]

---

## Raw Notes

[Any additional observations, console errors, timing notes, etc.]
```

## Generating the Report

### If Starting Fresh
1. Run a smoke test first
2. Walk through main user flows
3. Explore freely, noting observations
4. Compile findings into the report

### If Summarizing Previous Testing
1. Gather findings from previous smoke-test/walkthrough outputs
2. Organize by category
3. Add any missing screenshots
4. Write executive summary

## Categorizing Issues

### Critical
- App crashes
- Core functionality doesn't work
- Data loss possible
- Security issues

### Major
- Confusing UX that blocks users
- Features that fail silently
- Missing feedback/loading states
- Broken navigation

### Minor
- Visual inconsistencies
- Typos
- Suboptimal but functional UX
- Missing conveniences

## Tone

Be honest but constructive. This report should help the developer improve their app, not make them feel bad. Lead with what works, be specific about issues, and always suggest solutions.

Frame feedback as a user would:
- "As a new user, I wasn't sure what to do next..."
- "I expected clicking this would..., but instead..."
- "This worked great—I immediately understood..."

## After the Report

- "Here's your First User Report. Want to tackle the critical issues first?"
- "The main flows work! Should we test edge cases next?"
- "I noticed low agent-handle coverage. Want me to add handles to make future testing easier?"
