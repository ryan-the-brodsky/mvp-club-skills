# Agent Handles

Make your app AI-testable with semantic handles.

## Why Agent Handles?

When Claude (or any AI agent) tests your app using Playwright, it needs reliable ways to find and interact with UI elements. CSS classes change, text content varies, but **agent-handles are stable identifiers designed for automation**.

## The Pattern

```
{context}-{component}-{element}-{identifier}
```

Examples:
- `auth-login-button-submit`
- `auth-login-input-email`
- `dashboard-sidebar-link-settings`
- `checkout-cart-button-remove-item`

## Usage in HTML/JSX

```html
<button agent-handle="auth-login-button-submit">Sign In</button>
<input agent-handle="auth-login-input-email" placeholder="Email" />
```

## Skills

### `agent-handles:audit`
Scan your codebase for interactive elements (buttons, inputs, links, forms) that lack agent-handles.

### `agent-handles:suggest`
Get naming suggestions for elements following the convention.

### `agent-handles:add`
Have Claude add handles to your components.

## Part of the Work Loop

Agent handles enable the **Evaluate** phase—Claude can test your app as a real user would, clicking buttons and filling forms using these stable identifiers.

```
Articulate → Build → Prompt → Execute → Evaluate → Iterate
                                            ↑
                                    agent-handles enable this
```
