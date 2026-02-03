---
name: compare
description: Use this skill to create a side-by-side comparison of expected design vs actual implementation. Activate when users say "compare to mockup", "how close is it?", "PRD vs actual", "compare design to implementation". Invoke with screenshot-journal:compare.
---

# Screenshot Journal: Compare

You are creating a visual comparison between what was planned (mockup/design/PRD) and what was actually built.

## Prerequisites

- Playwright MCP required
- App running
- Reference image or description to compare against

## Finding the Reference

### From PRD
If there's a PRD with design descriptions or mockups:
- Reference the User Flow section
- Look for attached mockups or wireframes
- Use text descriptions to set expectations

### From External Design
If the user has a mockup file:
- "Compare against this Figma export"
- "Check against the design in /designs/homepage.png"

### From Previous State
Compare to an earlier screenshot:
- "Compare to yesterday's version"
- "How does this differ from the initial design?"

## Comparison Process

### 1. Capture Current State
Take a screenshot of the current implementation.

### 2. Load Reference
Get the comparison reference (file, description, or previous screenshot).

### 3. Create Comparison

```markdown
## Visual Comparison

### Reference (Expected)
[Mockup/design/previous screenshot]
*Source: PRD mockup / designs/homepage.png / 2024-01-14 capture*

### Current (Actual)
[Current screenshot]
*Captured: 2024-01-15 14:30*

---

### Analysis

| Aspect | Expected | Actual | Match |
|--------|----------|--------|-------|
| Layout | Two-column | Two-column | ✅ |
| Header | Logo left, nav right | Logo left, nav right | ✅ |
| CTA Button | Green, centered | Blue, left-aligned | ❌ |
| Typography | Sans-serif, 16px body | Sans-serif, 14px body | ⚠️ |

### Summary
**Overall match:** 85%

**Matches:**
- Overall layout structure
- Header placement
- Footer content

**Differences:**
- CTA button color (green → blue)
- CTA button position (centered → left)
- Body text slightly smaller than spec

**Suggestions:**
1. Update button color to match brand green (#22C55E)
2. Center the CTA in its container
3. Increase body font to 16px
```

## Comparison Types

### Layout Comparison
Focus on structure and positioning:
- Element placement
- Grid/column structure
- Spacing and alignment

### Style Comparison
Focus on visual design:
- Colors
- Typography
- Shadows and borders
- Icons and images

### Content Comparison
Focus on text and data:
- Headings and labels
- Placeholder content
- Data display format

### Responsive Comparison
Compare across viewport sizes:
- Desktop vs tablet vs mobile
- Breakpoint behavior

## When No Visual Reference Exists

If comparing against a text description from PRD:

```markdown
## Comparison: PRD Description vs Implementation

### PRD Says:
> "The dashboard should show a summary card at the top with total revenue,
> followed by a chart showing trends over the last 30 days."

### Implementation Shows:
- ✅ Summary card present at top
- ✅ Shows total revenue ($12,450)
- ⚠️ Chart shows 7 days, not 30
- ❌ Missing "last updated" timestamp mentioned in PRD

[Current screenshot]
```

## Output Format

Always include:
1. Visual side-by-side (if possible)
2. Structured analysis table
3. Clear match/mismatch indicators
4. Actionable suggestions

## After Comparison

- "Want me to help fix the differences?"
- "Should I update the PRD to reflect intentional changes?"
- "Ready to capture this as the new baseline?"

## Tone

Be objective and specific. The goal is to help the user see gaps between intention and implementation, not to judge quality. Note both what matches and what differs.
