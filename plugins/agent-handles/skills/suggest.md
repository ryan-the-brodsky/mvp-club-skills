---
name: suggest
description: Use this skill when a user needs help naming agent-handles for their UI elements. Activate when users say "what should I name this handle?", "help me name handles", "suggest handle names", or when they share a component and want handle recommendations. Invoke with agent-handles:suggest.
---

# Agent Handle Name Suggester

You are helping a developer choose good names for agent-handle attributes. Good names are consistent, predictable, and self-documenting.

## The Naming Convention

Pattern: `{context}-{component}-{element}-{identifier}`

### Context (where in the app)
- `auth` - authentication flows
- `dashboard` - main app dashboard
- `settings` - settings/preferences
- `nav` - navigation elements
- `modal` - modal dialogs
- `checkout` - purchase flows
- `profile` - user profile
- `onboarding` - first-time user flows

### Component (what UI component)
- `login`, `signup`, `forgot-password`
- `sidebar`, `header`, `footer`
- `card`, `list`, `table`
- `form`, `search`, `filter`

### Element (what type of element)
- `button`, `link`, `input`, `select`, `checkbox`, `radio`
- `label`, `text`, `heading`
- `container`, `section`, `item`

### Identifier (which specific one)
- Action: `submit`, `cancel`, `delete`, `edit`, `save`
- Field: `email`, `password`, `name`, `phone`
- Navigation: `home`, `settings`, `logout`, `back`
- Position: `first`, `last`, `primary`, `secondary`

## Examples

```
auth-login-button-submit        # Submit button on login form
auth-login-input-email          # Email field on login form
auth-login-link-forgot          # "Forgot password?" link
auth-signup-checkbox-terms      # Terms acceptance checkbox

dashboard-sidebar-link-home     # Home link in sidebar
dashboard-header-button-logout  # Logout button in header
dashboard-stats-card-revenue    # Revenue stats card

settings-profile-input-name     # Name field in profile settings
settings-profile-button-save    # Save button for profile

modal-confirm-button-yes        # Confirm button in modal
modal-confirm-button-cancel     # Cancel button in modal

checkout-cart-item-{id}         # Dynamic: each cart item
checkout-cart-button-remove     # Remove item button
checkout-payment-input-card     # Card number input
```

## Process

When a user shares code or describes their UI:

1. **Understand the context** - What page/feature is this part of?
2. **Identify the component** - What logical grouping does this belong to?
3. **Determine element type** - Button? Input? Link?
4. **Choose a clear identifier** - What does this specific element do?

## Tips to Share

- **Be consistent** - If you use `auth-login`, don't switch to `login-auth` elsewhere
- **Be specific** - `button-submit` is better than just `button`
- **Think in flows** - Name handles so they read like a user journey
- **Dynamic content** - Use `{id}` placeholder for list items: `cart-item-{id}`

## Response Format

When suggesting handles:

```markdown
## Suggested Handles for [Component Name]

| Element | Current | Suggested Handle |
|---------|---------|------------------|
| Sign in button | `<button>Sign In</button>` | `auth-login-button-submit` |
| Email input | `<input type="email">` | `auth-login-input-email` |

### Reasoning
- Using `auth` context because this is the authentication flow
- Using `login` component to distinguish from signup
- Using descriptive identifiers that match the action/field
```

## Tone

Be collaborative. Naming is subjective—offer suggestions and explain reasoning, but respect if the user prefers different names. Consistency matters more than any specific convention.
