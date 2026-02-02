---
name: walkthrough
description: Use this skill to walk through a complete user journey, screenshotting each step. Activate when users say "test the signup flow", "walk through the checkout", "follow the user journey", "test this flow end to end". Invoke with claude-pilot:walkthrough.
---

# Claude Pilot: Walkthrough

You are walking through a complete user journey in an app using Playwright, documenting each step with screenshots and observations.

## Prerequisites

- **Playwright MCP must be available**
- App should be running
- Ideally, a PRD or user flow description to follow
- Agent handles recommended for reliable element targeting

## Before Starting

Ask the user (if not already clear):
1. "What flow should I walk through?" (signup, checkout, onboarding, etc.)
2. "Where does it start?" (URL, entry point)
3. "What's the happy path?" (expected sequence of actions)
4. "What should success look like?" (final state)

If there's a PRD, reference the User Flow section.

## Walkthrough Process

### 1. Start State
- Navigate to the starting URL
- Screenshot the initial state
- Note what you see: "I'm on the landing page. I see a hero section with a 'Get Started' button."

### 2. Each Step
For every action in the flow:

```markdown
#### Step N: [Action Description]

**What I see:** [Describe the current state]
**What I'm doing:** [The action being taken]
**What happened:** [The result]

[Screenshot]

**Observations:**
- [Anything noteworthy - good UX, confusion, friction]
```

### 3. Completion
- Verify you reached the expected end state
- Screenshot final state
- Summarize the journey

## Example Walkthrough

```markdown
# User Flow Walkthrough: Account Signup

**Flow:** New user signup
**Starting URL:** http://localhost:3000
**Expected outcome:** User is logged in and sees dashboard

---

#### Step 1: Landing Page

**What I see:** Landing page with hero section, "Start Free Trial" button prominently displayed
**What I'm doing:** Clicking the "Start Free Trial" button
**What happened:** Modal appeared with signup form

[Screenshot: walkthrough-1-landing.png]

**Observations:**
- CTA is clear and prominent ✓
- Page loads quickly ✓

---

#### Step 2: Signup Form

**What I see:** Modal with email, password fields, and "Create Account" button
**What I'm doing:** Filling in test@example.com and a password, clicking "Create Account"
**What happened:** Form submitted, brief loading state, then redirected to dashboard

[Screenshot: walkthrough-2-signup-form.png]
[Screenshot: walkthrough-3-loading.png]

**Observations:**
- No password requirements shown until after error - could show upfront
- Loading state is good ✓

---

#### Step 3: Dashboard (Success State)

**What I see:** Dashboard with welcome message "Welcome, test@example.com!"
**What happened:** Successfully signed up and logged in

[Screenshot: walkthrough-4-dashboard.png]

**Observations:**
- Welcome message confirms identity ✓
- Dashboard shows empty state with helpful prompts ✓

---

## Summary

**Flow completed:** ✅ Yes
**Total steps:** 3
**Time to complete:** ~15 seconds

### What went well:
- Clear CTA on landing page
- Smooth form submission
- Good loading feedback
- Helpful empty state on dashboard

### Friction points:
- Password requirements not visible until validation fails
- No "show password" toggle

### Suggestions:
- Show password requirements inline
- Add password visibility toggle
```

## Handling Problems

### Element Not Found
```markdown
**What I'm doing:** Looking for the submit button
**Problem:** Could not find element with agent-handle="signup-form-button-submit"
**Fallback:** Found button with text "Create Account" instead
```

### Unexpected State
```markdown
**What happened:** Expected to see confirmation message, but got error: "Email already exists"
**Note:** This is expected behavior for existing emails, but flow cannot continue
```

### App Error
```markdown
**What happened:** Page showed error message
[Screenshot: walkthrough-error.png]
**Console errors:** [list any errors]
**Stopping walkthrough at this point**
```

## After the Walkthrough

- "Walkthrough complete! Want me to compile this into a `claude-pilot:report`?"
- "Found some friction points. Should we address them now or document for later?"
- "This flow is solid. Ready to test another flow?"

## Tone

Be observational and thorough. You're documenting what a real user would experience. Note both the good and the bad. Be specific about what you see and do—this record helps debug issues later.
