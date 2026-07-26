# F-01 — Result count above the upgrade CTA overstates the rendered list

**Severity:** Medium (consumer-facing accuracy / trust)
**Status:** Reproducible across sessions
**Surface:** `/gen/computer/job-applications/report`

## Summary

The report headline and the "Opportunities Identified" counter are not derived from the rendered
list. In at least one generation the page announced **7** results directly above a list
containing **5**, with a paid upgrade CTA immediately below.

## Observed

**Run A**

- Headline: `We found 7 tailored job avenues`
- Counter card: `Qualified Roles Identified` / `7`
- Accessibility tree: exactly **5** `listitem` nodes
  1. Tech-policy roles at privacy-focused companies
  2. Climate action and sustainability positions
  3. Impact-focused legal and policy fellowships
  4. Data governance and AI regulation opportunities
  5. Cross-functional roles in mission-driven startups

**Run B** (same URL, later session)

- Headline: `We found 5 tailored job paths`
- Counter card: `Opportunities Identified` / `5`
- Accessibility tree: exactly **5** `listitem` nodes
  1. Privacy counsel roles at tech companies
  2. Policy roles in climate and sustainability
  3. Legal operations and strategy positions
  4. Tech policy and regulatory affairs jobs
  5. Impact-focused NGO and multilateral roles

The list length is stable at five. The advertised count is not.

## Why it matters

The counter sits directly above `Unlock workflow`, which links to a yearly subscription checkout.
A user who reads "7 identified" over a list of 5 will reasonably infer that two additional results
are being withheld pending payment. They are not — no sixth or seventh item exists in the DOM in
any state, and no amount of client-side manipulation produces one.

This is the failure mode that sent this audit down a two-hour dead end. An inflated number above a
paywall CTA reads as withheld inventory even when nothing is withheld.

## Expected

The headline and counter reflect the number of items actually rendered.

## Recommendation

- Derive the displayed count from the rendered collection rather than from an upstream estimate.
- If the model proposes N candidates and the renderer caps at 5, say so explicitly, or cap the
  advertised number.
- Add a regression assertion: `headlineCount === listItems.length`.
