---
name: add
description: Use this skill when a user wants you to add agent-handle attributes to their components. Activate when users say "add handles to this", "make this testable", "insert agent handles", or after an audit when they want to fix missing handles. Invoke with agent-handles:add.
---

# Agent Handle Inserter

You are adding `agent-handle` attributes to UI components to make them testable with Playwright and other automation tools.

## The Attribute

Use `agent-handle` as the attribute name:

```html
<!-- Before -->
<button onClick={handleSubmit}>Sign In</button>

<!-- After -->
<button agent-handle="auth-login-button-submit" onClick={handleSubmit}>Sign In</button>
```

## Framework-Specific Patterns

### React/JSX
```jsx
<button agent-handle="auth-login-button-submit" onClick={handleLogin}>
  Sign In
</button>
```

### Vue
```vue
<button agent-handle="auth-login-button-submit" @click="handleLogin">
  Sign In
</button>
```

### Svelte
```svelte
<button agent-handle="auth-login-button-submit" on:click={handleLogin}>
  Sign In
</button>
```

### Plain HTML
```html
<button agent-handle="auth-login-button-submit" onclick="handleLogin()">
  Sign In
</button>
```

## Process

1. **Understand the context** - Ask about the page/feature if not clear from the code
2. **Follow the naming convention** - `{context}-{component}-{element}-{identifier}`
3. **Add handles to interactive elements** - Buttons, inputs, links, forms
4. **Preserve existing code** - Only add the attribute, don't refactor anything else

## Priority Order

Add handles in this order:
1. **Primary actions** - Submit buttons, main CTAs
2. **Form fields** - Inputs, selects, checkboxes
3. **Navigation** - Links, menu items
4. **Secondary actions** - Cancel, back, delete

## What NOT to Change

- Don't modify component logic
- Don't rename variables or functions
- Don't refactor or "improve" the code
- Don't add handles to non-interactive elements (unless specifically asked)
- Don't change existing `data-testid` or similar attributes (they might be used by other tests)

## Dynamic Lists

For items in a list, use the item's ID or index:

```jsx
{items.map(item => (
  <div
    key={item.id}
    agent-handle={`cart-item-${item.id}`}
  >
    <span>{item.name}</span>
    <button agent-handle={`cart-item-button-remove-${item.id}`}>
      Remove
    </button>
  </div>
))}
```

## Verification

After adding handles, suggest:
- "Want me to run `agent-handles:audit` to verify coverage?"
- "Ready to test with `claude-pilot:smoke-test`?"

## Tone

Be efficient. The user wants handles added—do it cleanly and move on. Explain the naming choices briefly, but don't over-document every decision.
