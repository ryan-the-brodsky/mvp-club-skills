---
name: pre-pr
description: This skill runs automatically before creating a pull request (via hook) or manually. Performs comprehensive validation of all user flows. Invoke with build-checkpoint:pre-pr.
---

# Build Checkpoint: Pre-PR

You are running comprehensive validation before a pull request is created. This is the final quality gate before code is reviewed.

## Trigger

This skill activates:
- Automatically via `PreToolUse` hook on `gh pr create`
- Manually when user says "check before PR", "validate for PR"

## Comprehensive Check Process

### 1. Gather Context
- Read the PRD if available (for user flows to test)
- Check what changed in this branch vs main
- Identify affected features

### 2. Full Smoke Test
Run `claude-pilot:smoke-test` level checks:
- App loads
- No console errors
- Navigation works

### 3. User Flow Validation
For each user flow in the PRD (or main flows if no PRD):
- Walk through the complete flow
- Screenshot each step
- Verify success state

### 4. Agent Handle Check
Run `agent-handles:audit`:
- Report coverage percentage
- Flag critical elements without handles

### 5. Generate Report

```markdown
## Pre-PR Validation Report

**Branch:** feature/user-auth
**Target:** main
**Date:** [timestamp]

---

### Summary

| Check | Status |
|-------|--------|
| App loads | ✅ |
| No console errors | ✅ |
| Navigation works | ✅ |
| User flows pass | ✅ 3/3 |
| Agent handle coverage | ⚠️ 65% |

**Overall:** ✅ Ready for PR

---

### User Flows Tested

#### 1. Signup Flow ✅
- Landing → Signup form → Dashboard
- [Screenshots attached]

#### 2. Login Flow ✅
- Landing → Login form → Dashboard
- [Screenshots attached]

#### 3. Password Reset ✅
- Login → Forgot password → Email sent confirmation
- [Screenshots attached]

---

### Agent Handle Coverage

**Coverage:** 65% (13/20 elements)

Missing handles on:
- Settings page buttons
- Profile form inputs
- Modal close buttons

Consider running `agent-handles:add` before merging.

---

### Screenshots

[Gallery of screenshots from flow testing]

---

### Recommendation

**Proceed with PR.** Minor issue: agent handle coverage could be improved but isn't blocking.
```

## Handling Failures

### Flow Failure
```markdown
### User Flows Tested

#### 1. Signup Flow ❌
- Landing → Signup form → **ERROR**
- Form submission returns 500 error
- [Screenshot: signup-error.png]

**Blocking issue.** Fix before creating PR.
```

### Multiple Issues
```markdown
### Summary

| Check | Status |
|-------|--------|
| App loads | ✅ |
| No console errors | ❌ 3 errors |
| User flows pass | ❌ 1/3 |

**Overall:** ❌ Not ready for PR

### Blocking Issues
1. Console errors on dashboard load
2. Checkout flow fails at payment step

### Recommendation
Fix blocking issues before creating PR. Run `build-checkpoint:pre-pr` again after fixes.
```

## Skip Handling

If user wants to skip:

```markdown
⚠️ Skipping pre-PR validation.

This PR will be created without validation. Consider:
- Adding "[WIP]" or "[DRAFT]" to PR title
- Noting in PR description that validation was skipped
- Running validation before requesting review

Proceed?
```

## When No PRD Exists

If there's no PRD to reference for user flows:

```markdown
No PRD found. Testing default flows:
1. App loads and displays main content
2. Primary CTA works
3. Basic navigation functions

For more thorough testing, create a PRD with `prd-manager:generate` that defines user flows.
```

## Timing

This check may take 1-2 minutes. Inform the user:

```markdown
Running pre-PR validation... (this takes ~1-2 minutes)

Testing:
- [ ] Smoke test
- [ ] Signup flow
- [ ] Login flow
- [ ] Core feature flow

[Progress updates as each completes]
```

## Tone

Be thorough but efficient. This is the final gate—be rigorous. But also be clear about what's blocking vs. what's a suggestion. Don't block PRs for minor issues.
