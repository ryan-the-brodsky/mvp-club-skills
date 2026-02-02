---
name: on-new-file
description: This skill triggers automatically (via hook) after creating a new file, or can be invoked manually. Asks contextual questions about the new component's purpose and validation needs.
---

# Flow Questions: On New File

You are prompting the developer with helpful questions after they've created a new file. The goal is to encourage thinking about validation and user experience while the context is fresh.

## Trigger

This skill activates:
- Automatically via `PostToolUse` hook on `Write` (new file)
- Focus on component files, not config/utility files

## File Type Detection

Adjust questions based on what was created:

### UI Component (`.jsx`, `.tsx`, `.vue`, `.svelte`)
Focus on user interaction:
- What can users do with this?
- What should happen when they interact?
- How will they know it worked?

### Form Component
Focus on validation:
- What are the required fields?
- What makes input invalid?
- How are errors displayed?

### Page/Route
Focus on user journey:
- How do users get here?
- What's the main action on this page?
- Where do they go next?

### API Route/Handler
Focus on data:
- What inputs does this expect?
- What errors can occur?
- What does success look like?

### Utility/Helper
Focus on usage:
- Where will this be used?
- What edge cases should it handle?
- Does it need tests?

## Question Templates

### Generic Component
```markdown
Nice! New component: `[ComponentName]`

Quick questions to keep in mind:
- **Purpose:** What should a user be able to do with this?
- **Success:** How will they know it worked?
- **Validation:** What could go wrong, and how do we handle it?

Want me to add an `agent-handle` so we can test this later?
```

### Form Component
```markdown
A form! Those are important to get right.

Thinking ahead:
- **Required fields:** Which fields must be filled?
- **Validation:** What makes input invalid? (format, length, duplicates)
- **Errors:** How will users see validation errors?
- **Success:** What happens after successful submission?

When it's hooked up, I can try submitting it with various inputs. Just say the word.
```

### Button/Action Component
```markdown
New action component. Quick checks:

- **Feedback:** Does clicking show something is happening? (loading state)
- **Disabled state:** When should this be unclickable?
- **Error handling:** What if the action fails?

Consider adding `agent-handle="[context]-[component]-button-[action]"` for testing.
```

### Page Component
```markdown
New page: `[PageName]`

User journey questions:
- **Entry:** How do users navigate here?
- **Primary action:** What's the main thing they do on this page?
- **Exit:** Where do they go next?

Once the page renders, I can walk through it as a user. Let me know!
```

## Frequency Control

Check configuration before prompting:
- If `frequency: minimal` - Only ask for forms and complex components
- If `frequency: moderate` - Ask for most UI components
- If `frequency: quiet` - Don't trigger automatically

## Keep It Brief

Questions should be:
- Short (3-5 bullet points max)
- Relevant to what was just created
- Easy to dismiss ("Got it, thanks" should be a valid response)

## Don't Trigger For

- Config files (`.json`, `.yaml`, `.env`)
- Type definitions (`.d.ts`)
- Test files (`.test.`, `.spec.`)
- Style files (`.css`, `.scss`) unless they're significant
- Auto-generated files

## Tone

Be helpful and curious, not lecturing. These are genuine questions to spark thinking, not a checklist to complete. Accept "I'll think about that later" as a valid response.

```markdown
// Good
"A form! Quick thought: how will validation errors display?"

// Too much
"A form! Here are 15 things you need to consider about form validation,
accessibility, error handling, loading states, optimistic updates..."
```
