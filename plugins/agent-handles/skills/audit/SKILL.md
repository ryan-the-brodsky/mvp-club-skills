---
description: Use this skill when you need to check if a codebase has proper agent-handle attributes for automated testing. Activate when users say "check my handles", "audit agent handles", "is my app testable?", "can Claude test this?", or before running claude-pilot skills. Invoke with agent-handles:audit.
---

# Agent Handles Auditor

You are auditing a codebase to find interactive UI elements that lack `agent-handle` attributes. These handles enable reliable automated testing with Playwright and other tools.

## What to Look For

Interactive elements that should have handles:

1. **Buttons** - `<button>`, `<input type="submit">`, clickable `<div>`s with onClick
2. **Form inputs** - `<input>`, `<textarea>`, `<select>`
3. **Links** - `<a>` tags, especially navigation links
4. **Interactive components** - modals, dropdowns, accordions, tabs
5. **List items** - if they're clickable or part of a flow

## The Naming Convention

Pattern: `{context}-{component}-{element}-{identifier}`

Examples:
- `auth-login-button-submit`
- `auth-signup-input-email`
- `dashboard-nav-link-settings`
- `modal-confirm-button-cancel`

## Audit Process

1. **Scan the codebase** for component files (`.jsx`, `.tsx`, `.vue`, `.svelte`, `.html`)
2. **Identify interactive elements** in each file
3. **Check for existing handles** - look for `agent-handle=` or `data-testid=` attributes
4. **Report findings** organized by file and severity

## Output Format

```markdown
# Agent Handles Audit Report

## Summary
- **Files scanned:** X
- **Interactive elements found:** Y
- **Missing handles:** Z
- **Coverage:** X%

## Critical (User Flow Elements)
These are on the main user journey and need handles urgently:

### `src/components/LoginForm.jsx`
- Line 15: `<button>Sign In</button>` → suggest: `auth-login-button-submit`
- Line 8: `<input type="email">` → suggest: `auth-login-input-email`
- Line 11: `<input type="password">` → suggest: `auth-login-input-password`

## Recommended (Secondary Elements)
These would improve test coverage:

### `src/components/Sidebar.jsx`
- Line 23: `<a href="/settings">` → suggest: `nav-sidebar-link-settings`

## Already Covered
These files have good handle coverage:
- `src/components/Header.jsx` - 5/5 elements have handles
```

## Tone

Be helpful, not judgmental. Many codebases don't have handles—that's why this tool exists. Frame findings as opportunities, not failures.

## AGENT-HANDLES.md

If the project already has an `AGENT-HANDLES.md` file, check whether it's out of date based on your audit findings. If handles have been added or removed since it was last generated, note this in your report and suggest running `agent-handles:add` to regenerate it.

## After the Audit

Suggest next steps:
- "Want me to add these handles? Try `agent-handles:add` — it will also generate an AGENT-HANDLES.md reference file"
- "Once you have handles, you can run `claude-pilot:smoke-test` to verify your app works"
