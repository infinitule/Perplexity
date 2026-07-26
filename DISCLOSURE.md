# Disclosure

## Posture

This repository was **published without prior vendor coordination.** That is a deliberate choice by
the author and it is stated plainly rather than dressed up as a 0-day drop or a completed 90-day
clock, neither of which happened.

The tradeoff, honestly: F-02 (product prompt in a query string) is the finding a competitor would
find interesting, and publishing it before Perplexity can rotate the parameter hands it over
immediately. The counterargument is that the parameter is already visible to every visitor who
hovers the button, so publication changes reach rather than availability.

Nothing here is a vulnerability in the security sense. There is no exploit, no user data exposure,
no authentication weakness, and no circumvention technique. Read the findings before deciding this
is a disclosure repo in the CVE sense — it is a UX and hygiene audit.

**Recommended next step for anyone forking this posture:** send the report below the same day you
publish, so the vendor learns about it from you rather than from a search alert.

## Contact routes

- Security: `security@perplexity.ai`
- Bug bounty, if in scope: check `perplexity.ai/.well-known/security.txt` before filing
- Product feedback (F-01, F-03, F-04 are product bugs, not security): in-app feedback

## Report draft

> **Subject:** UX and information-disclosure findings — job-report upgrade panel
>
> Hello,
>
> I audited the upgrade panel on the generated job-report surface
> (`/gen/computer/job-applications/report`) and found four issues. None are security
> vulnerabilities; no circumvention was performed or is being published. Details and repro steps:
> <REPO URL>
>
> **F-01 (Medium).** The headline and "Opportunities Identified" counter are not derived from the
> rendered list. One generation displayed "7" directly above five cards, with the subscription CTA
> immediately below. Because the count sits above a paid upsell, an inflated number reads as
> withheld results. It is a display bug, but it is one that costs user trust in a purchase moment.
>
> **F-02 (Low–Medium).** The `Unlock workflow` link carries the full workflow prompt, URL-encoded,
> in `redirect_path`. It is readable without authentication, and because it lives in a URL it
> propagates to browser history, `Referer` headers, analytics, and proxy logs. It also interpolates
> the user-supplied LinkedIn profile URL into that same parameter, carrying PII along the same
> paths. Suggest a server-side template ID instead.
>
> **F-03 (Low).** The panel is viewport-positioned rather than container-constrained; below ~75%
> zoom or in narrow portrait windows it detaches and clips against the top of the viewport.
>
> **F-04 (Low–Medium).** The panel has no dismiss control and no Escape handler — its only
> interactive element is the checkout link — while its scrim covers list items the user is already
> entitled to. Relevant to WCAG 2.1 SC 1.4.10 and to the dialog pattern generally.
>
> Happy to clarify any of these or hold detail if you'd prefer a coordinated timeline on F-02.
>
> — <YOUR NAME>

## Timeline

| Date | Event |
|------|-------|
| 2026-07-26 | Findings observed |
| 2026-07-26 | Repository published |
| _pending_ | Report sent to vendor |
| _pending_ | Vendor response |
