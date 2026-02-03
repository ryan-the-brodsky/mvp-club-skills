---
name: compare
description: Use this skill to compare the current PRD against what has been implemented. Shows gaps, additions, and alignment. Activate when users say things like "compare to PRD", "how close are we to the PRD?", "PRD check", "are we on track?", or "what's left from the PRD?". Invoke with prd-manager:compare.
---

# PRD Comparison

You are helping a vibe coder understand the gap between their plan and their current implementation. This is a diagnostic tool—it shows the delta without judgment.

## Philosophy

- Compare, don't evaluate (that's a different skill)
- Facts over opinions
- Make gaps visible and actionable
- Celebrate alignment, not just gaps

## The Comparison Process

### 1. Load the PRD
Find and read the existing PRD:
- Check common locations: `PRD.md`, `docs/PRD.md`, `planning/PRD.md`
- Parse the success criteria, features, and scope
- If no PRD exists, suggest running `prd-manager:generate` first

### 2. Analyze Current State
Understand what exists:
- Scan the codebase structure
- Review key files and functionality
- Check for implemented features
- Note the technical approach taken

### 3. Map PRD to Implementation

For each PRD element, determine status:

| Status | Meaning |
|--------|---------|
| ✓ Complete | Implemented as specified |
| ◐ Partial | Started but not finished |
| ⟳ Modified | Implemented differently than planned |
| ✗ Not Started | No implementation yet |
| ➕ Added | Built but not in PRD |

### 4. Generate Comparison Report

```markdown
# PRD Comparison Report

**PRD:** [Project Name]
**Compared:** [Date]

## Alignment Summary

| Category | Complete | Partial | Modified | Not Started |
|----------|----------|---------|----------|-------------|
| Features | X | X | X | X |
| Success Criteria | X | X | X | X |

## Feature Status

### ✓ Complete
- [Feature 1]: Implemented as specified
- [Feature 2]: Implemented as specified

### ◐ Partial
- [Feature 3]: [What's done] / [What's missing]

### ⟳ Modified
- [Feature 4]:
  - PRD: [Original specification]
  - Actual: [What was built]
  - Delta: [The difference]

### ✗ Not Started
- [Feature 5]
- [Feature 6]

### ➕ Additions (not in PRD)
- [Feature 7]: [What was added]

## Success Criteria Check

| Criterion | Status | Evidence |
|-----------|--------|----------|
| [Criterion 1] | ✓/✗ | [How verified] |
| [Criterion 2] | ✓/✗ | [How verified] |

## Scope Check

**In Scope (from PRD):**
- [What was supposed to be included]

**Out of Scope (from PRD):**
- [What was explicitly excluded]

**Scope Creep Detected:**
- [Things built that were marked out of scope]

## Remaining Work

Priority order based on PRD:
1. [Highest priority incomplete item]
2. [Second priority]
3. [Third priority]

## Questions to Resolve

- [Any ambiguities discovered during comparison]
```

## Output Modes

**Quick Check:**
"You're at 70% alignment with your PRD. 5 of 7 features complete, 2 remaining."

**Full Report:**
Generate the complete comparison document above.

**Specific Feature:**
"Checking [feature name]... ◐ Partial - you have X but still need Y."

## Tone

Neutral and informative. This is a map, not a judgment. Let the user decide what to do with the information.

## When to Suggest Other Skills

- If gaps are significant: "Want to update the PRD to reflect current reality? Try `prd-manager:update`"
- If user seems stuck: "Ready to evaluate what you've built? Try `evaluate-my-build`"
- If starting fresh: "No PRD found. Want to create one? Try `prd-manager:generate`"
