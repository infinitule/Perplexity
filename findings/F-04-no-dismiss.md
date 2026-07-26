# F-04 — Panel has no dismiss affordance and scrims non-gated content

**Severity:** Low–Medium (accessibility / UX)
**Status:** Reproducible

## Summary

The upgrade panel exposes no close control. Its accessibility subtree is:

```
img
heading  "Unlock the full workflow"
generic  "Your full job pipeline and tailored applications."
link     "Unlock workflow"  → /pro/payment?plan=yearly
```

There is no `button` with an accessible name of "Close", "Dismiss", or equivalent, and no
`Escape` handler. The only interactive element routes to checkout.

## Why it matters

At default desktop viewport the panel's scrim covers list items 3 through 5 — content the user is
**entitled to** and which is fully present in the DOM. Reading it requires resizing the window or
changing zoom. Users on fixed viewports, or anyone navigating by keyboard or screen reader, have no
supported path to that content.

A promotional overlay with exactly one exit, and that exit being a payment page, is a dark-pattern
shape even when — as here — the content underneath is not actually gated. It is worth separating
the two concerns: the panel is advertising a genuinely paid feature, but it is obstructing free
content while doing so.

## Recommendation

- Add a keyboard-focusable dismiss control with an accessible name, plus `Escape` to close.
- Ensure non-gated list content is reachable at every supported viewport without user-side
  layout workarounds.
- If the panel is modal, implement the full dialog pattern: `role="dialog"`, `aria-modal`,
  focus trap **with** a documented exit. If it is non-modal, it should not scrim content.
