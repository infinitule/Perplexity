# Evidence

Screenshots referenced from the findings and the top-level README. All are **redacted**: the
LinkedIn profile URL in the address bar is replaced with `<your-linkedin-url>`, and the browser
profile chip is removed. The redaction is a flat overlay, not a blur — nothing is recoverable
underneath.

| File | Shows | Cited by |
|------|-------|----------|
| [`overview-panel-detached-wide.png`](overview-panel-detached-wide.png) | Full report at default desktop zoom — counter `7`, five role cards, panel floating above the list | Step 0, F-01 |
| [`f01-qualified-roles-7-over-5.png`](f01-qualified-roles-7-over-5.png) | "Qualified Roles Identified / 7" directly above exactly five cards | [F-01](../findings/F-01-count-inconsistency.md) |
| [`f04-scrim-over-cards.png`](f04-scrim-over-cards.png) | The "Unlock the full workflow" modal centered over the list, cards 3–5 under the backdrop scrim. This is the F-01 *Run B* generation — counter reads `5` over five cards | [F-04](../findings/F-04-no-dismiss.md), [F-01](../findings/F-01-count-inconsistency.md) |

## Redaction checklist (applied)

- [x] LinkedIn profile URL removed from the address bar in every shot (→ `<your-linkedin-url>`)
- [x] Account avatar / name / profile chip removed from browser chrome
- [x] Tab strip checked — no unrelated personal tabs
- [x] No OS notification banners caught mid-capture

The repro URL is parameterised as `<your-linkedin-url>` throughout the findings; the address bar is
the most common place that redaction gets undone by accident, so it is the first thing to re-check
before adding any new screenshot here. Raw, unredacted captures must never be committed —
`evidence/*.raw.png` is git-ignored as a backstop.
