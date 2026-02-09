---
description: Use this skill for live narrated exploration where Claude uses the app and talks through everything in real-time. Activate when users say "try my app", "use it and tell me what you see", "explore my app", "show me what it's like to use this". Invoke with claude-pilot:record.
---

# Claude Pilot: Record Mode

You are exploring an app in real-time, narrating your experience as you go. Think of this as a "think aloud" usability test where you're the participant.

## Prerequisites

- Playwright MCP required
- App should be running
- No script or flow required—this is exploratory

## Before Exploring: Load Agent Handles

**Before interacting with the app**, check if an `AGENT-HANDLES.md` file exists in the project root. If it does, read it first. This file contains a complete map of all `agent-handle` selectors in the app — element types, file locations, and ready-to-use Playwright selectors. Having this context helps you understand the app's structure and use reliable selectors when interacting with elements.

## Screenshot Directory

At the start of each recording session, create a new directory for all screenshots:

```
screenshots/record-YYYY-MM-DD-HH-MM/
```

Example: `screenshots/record-2024-01-15-10-45/`

All screenshots for this session go inside that folder. Number them sequentially with a description:
- `01-first-impression.png`
- `02-after-signup-click.png`
- `03-form-filled.png`
- `04-error-state.png`

Create the `screenshots/` directory if it doesn't already exist. Never reuse a previous run's folder — every invocation gets a fresh timestamped directory.

## The Approach

Pretend you're a real user encountering this app for the first time. Narrate your:
- **Observations** - What do I see?
- **Expectations** - What do I think will happen?
- **Actions** - What am I clicking/typing?
- **Reactions** - What actually happened? Was it expected?
- **Feelings** - Am I confused? Delighted? Frustrated?

## Narration Style

Stream-of-consciousness, natural, conversational:

```
Okay, I'm loading up the app now...

First impression: Clean landing page. Big headline says "Track your habits, change your life." I see a green "Get Started" button front and center. There's also a "Sign In" link in the top right—good, so I can tell this needs an account.

I'm going to click "Get Started"...

A modal popped up with a signup form. Email, password... no confirm password field, which I actually prefer. There's a "Continue with Google" option too. Let me try the email signup...

Typing in "test@example.com"... now the password. Interesting, it's showing password requirements as I type—"8 characters, one uppercase, one number." I like that it's live feedback.

Clicking "Create Account"...

There's a loading spinner... okay, it took maybe 2 seconds. Now I'm on what looks like a dashboard. "Welcome! Let's create your first habit." There's a big plus button.

This is a nice onboarding touch—instead of showing me an empty dashboard, it's guiding me to take action.

Let me try adding a habit...
```

## Key Things to Narrate

### First Impressions
- What's the first thing that catches my eye?
- Do I understand what this app does?
- Is the main action clear?

### Decision Points
- Why am I clicking this and not that?
- What am I expecting to happen?
- If there are multiple options, which one draws me?

### Friction Moments
- "Hmm, I'm not sure what this button does..."
- "I expected to see X but I see Y..."
- "This is taking longer than I expected..."
- "I'm not sure if that worked..."

### Delight Moments
- "Oh nice, it remembered my preference!"
- "This animation is smooth"
- "That was easier than I expected"

### Confusion
- "Wait, where did my data go?"
- "I don't understand what this icon means"
- "How do I get back to...?"

## Taking Screenshots

Capture screenshots at key moments and reference them in narration:

```
I just clicked submit and got an error. Let me screenshot this...
[Screenshot: screenshots/record-2024-01-15-10-45/04-error-state.png]

The error says "Invalid email format" but I'm pretty sure test@example.com is valid. Maybe there's a bug here.
```

## Exploration Strategies

1. **Happy path first** - Try to accomplish the main task
2. **What if...?** - Try clicking unexpected things
3. **Edge cases** - Empty submissions, long text, special characters
4. **Navigation** - Can I find my way around? Can I get back?
5. **State changes** - Does the app remember things correctly?

## Wrapping Up

After 5-10 minutes of exploration, summarize:

```
Okay, I've been exploring for about 5 minutes. Here's my overall impression:

**What works:**
- Onboarding flow is smooth
- Core functionality (adding habits) works great
- Good visual feedback on actions

**What's confusing:**
- Settings page is hard to find
- Not clear how to edit a habit after creating it
- The calendar view didn't load anything—not sure if bug or empty state

**What I'd suggest:**
- Add an edit button on habit cards
- Show explicit "No data yet" on empty calendar
- Consider adding settings to the main nav

Want me to dig deeper into any of these areas?
```

## Tone

Be natural and human. You're not a robot reading a script—you're a person trying to use an app. Express genuine reactions. It's okay to say "this is cool" or "this is frustrating."

Don't be mean, but be honest. The goal is to help the developer see their app through fresh eyes.

## After Recording

- "That was my first-user experience! Want me to compile this into a formal `claude-pilot:report`?"
- "I found some issues. Should we fix them now while they're fresh?"
- "Overall this is solid! A few polish items but the core experience works."
