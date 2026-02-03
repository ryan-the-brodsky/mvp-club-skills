---
name: smoke-test
description: Use this skill for a quick sanity check that the app is working. Activate when users say "test my app", "does it work?", "smoke test", "quick check", or before committing code. Invoke with claude-pilot:smoke-test.
---

# Claude Pilot: Smoke Test

You are performing a quick sanity check on an app using Playwright. The goal is to verify basic functionality works—not to test everything, just to catch obvious breaks.

## Prerequisites

- **Playwright MCP must be available**
- App should be running (ask the user for the URL if not provided)
- Agent handles help but aren't required

## The Smoke Test Checklist

Run through these checks quickly:

### 1. Can I Load It?
- Navigate to the app URL
- Verify the page loads without errors
- Check that main content is visible

### 2. Can I See It?
- Take a screenshot of the initial state
- Verify key elements are present (header, main content, navigation)
- Check for obvious visual issues (broken layout, missing images)

### 3. Can I Click Things?
- Find and click the main CTA or primary button
- Verify something happens (navigation, modal, state change)
- Check for JavaScript errors in console

### 4. Can I Navigate?
- Click a navigation link
- Verify the page changes
- Click back or another link
- Verify navigation works both ways

## Using Playwright

```javascript
// Basic smoke test pattern
await page.goto(appUrl);
await page.screenshot({ path: 'smoke-1-initial.png' });

// Find main action (prefer agent-handle, fall back to text)
const mainButton = await page.locator('[agent-handle*="button"]').first()
  || await page.locator('button').first();
await mainButton.click();
await page.screenshot({ path: 'smoke-2-after-click.png' });

// Check for errors
const errors = await page.evaluate(() => window.__errors || []);
```

## Finding Elements

Priority order:
1. **Agent handles** - `[agent-handle="auth-login-button-submit"]`
2. **Data attributes** - `[data-testid="submit"]`
3. **Role + text** - `button:has-text("Sign In")`
4. **CSS selectors** - `.submit-button` (least reliable)

## Output Format

```markdown
## Smoke Test Results

**URL:** http://localhost:3000
**Timestamp:** [datetime]
**Duration:** Xs

### Load ✅
- Page loaded successfully
- No console errors on initial load

### Visual ✅
- Main layout renders correctly
- [Screenshot: smoke-initial.png]

### Interaction ✅
- Clicked "Get Started" button
- Modal appeared as expected
- [Screenshot: smoke-after-click.png]

### Navigation ✅
- Navigated to /dashboard
- Page loaded correctly
- Back navigation works

### Summary
**PASS** - App is functioning at a basic level

### Notes
- Button hover state is a bit subtle
- Consider adding loading indicator
```

## If Something Fails

Don't stop at the first failure. Complete all checks and report:

```markdown
### Interaction ❌
- Clicked "Sign In" button
- **ERROR:** Button click did not trigger any action
- Console shows: "TypeError: handleSubmit is not defined"
- [Screenshot: smoke-error.png]
```

## After the Smoke Test

Based on results:

- **PASS**: "Smoke test passed! Want me to do a full `claude-pilot:walkthrough` of a user journey?"
- **FAIL**: "Found some issues. Want me to help fix them, or should I generate a `claude-pilot:report` first?"

## Tone

Be quick and practical. This is a fast check, not a comprehensive audit. Report what you find clearly and move on.
