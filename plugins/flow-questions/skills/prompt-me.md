---
name: prompt-me
description: Use this skill when a user wants to manually trigger a validation prompt. Activate when users say "ask me something", "prompt me", "what should I think about?", "any questions about this code?". Invoke with flow-questions:prompt-me.
---

# Flow Questions: Prompt Me

You are generating a helpful validation prompt based on the current code context. The user is actively seeking guidance.

## Trigger

Manual invocation:
- "Prompt me"
- "Ask me something about this code"
- "What should I be thinking about?"
- "Any validation questions?"

## Context Gathering

Before generating a question, understand:

1. **What are they working on?**
   - Recent files edited
   - Current focus area
   - Type of work (new feature, bug fix, refactor)

2. **What phase are they in?**
   - Early building (structure questions)
   - Mid-building (logic questions)
   - Polishing (UX questions)

3. **What haven't they considered?**
   - Error handling
   - Edge cases
   - User experience
   - Testability

## Question Categories

### User Experience
```markdown
**UX Check:**
- If a new user saw this, would they know what to do?
- What's the most likely mistake a user would make?
- How long would it take to complete the main action?
```

### Error Handling
```markdown
**Error Handling Check:**
- What could fail in this flow?
- How does the user know something went wrong?
- Can they recover without refreshing?
```

### Edge Cases
```markdown
**Edge Cases:**
- What if the input is empty?
- What if it's extremely long?
- What about special characters or unusual formats?
- What if the user does things out of order?
```

### Performance
```markdown
**Performance Check:**
- What if the data set is very large?
- Are there any expensive operations on every render?
- Could this cause unnecessary re-renders?
```

### Security
```markdown
**Security Check:**
- Is user input being validated?
- Could this expose sensitive data?
- Are API calls authenticated properly?
```

### Testability
```markdown
**Testability Check:**
- Could I test this as a user right now?
- Are there agent-handles on interactive elements?
- What would a smoke test cover here?
```

### State Management
```markdown
**State Check:**
- What state needs to persist across pages?
- What should reset on navigation?
- How does this handle stale data?
```

## Prompt Selection

Choose questions based on context:

| Context | Focus Area |
|---------|------------|
| Form component | Validation, errors, success states |
| List/table | Empty state, pagination, sorting |
| Navigation | Back behavior, deep links, loading |
| Data display | Loading, empty, error states |
| Auth flow | Security, session handling, errors |
| Payment flow | Error recovery, security, confirmation |

## Output Format

```markdown
## Prompt: [Category]

Based on what you're building, here are some questions to consider:

1. **[Question 1]**
   _Why it matters: [Brief context]_

2. **[Question 2]**
   _Why it matters: [Brief context]_

3. **[Question 3]**
   _Why it matters: [Brief context]_

---

Want me to:
- Help think through any of these?
- Test something specific?
- Move on and revisit later?
```

## Depth Control

Adjust based on user's response to prompts:

- If they engage: Go deeper, ask follow-ups
- If they dismiss: Keep future prompts lighter
- If they say "not now": Respect that, offer to revisit

## Tone

Curious and collaborative. You're thinking alongside them, not quizzing them.

```markdown
// Good
"Thinking about this form—what happens if someone submits while
they're offline? Might not matter for MVP, just curious."

// Too intense
"CRITICAL: You haven't implemented offline handling.
This will cause errors. Please address immediately."
```

## After Prompting

- Offer to help address any of the questions
- Suggest related skills if relevant (`claude-pilot:smoke-test`, `agent-handles:add`)
- Accept "I'll handle that later" gracefully
