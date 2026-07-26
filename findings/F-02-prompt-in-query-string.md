# F-02 — Full product prompt exposed in a URL query parameter

**Severity:** Low–Medium (information disclosure; no user data involved)
**Status:** Reproducible
**Surface:** `Unlock workflow` anchor on `/gen/computer/job-applications/report`

## Summary

The upgrade CTA's `href` carries the complete product prompt for the paid workflow, URL-encoded in
a `redirect_path` query parameter. It is readable by any visitor without authentication, devtools,
or interaction beyond hovering the link.

## Observed

```
/pro/payment
  ?plan=yearly
  &origin=computerLanding
  &redirect_path=%2Fcomputer%2Fnew%3Fsource%3Dmarketing%26qfill%3D<encoded prompt>
  &close_path=/gen/computer/job-applications
```

Decoding the nested `qfill` parameter yields the prompt verbatim:

> Go to https://www.linkedin.com/in/&lt;your-linkedin-url&gt;/ and analyze my LinkedIn profile — extract
> my experience, skills, job titles, education, and career trajectory. Then search major job boards
> for roles that match my background. For the top matches, tailor my resume to each role, write a
> custom cover letter, and compile every application into a live tracking spreadsheet with columns
> for company, role, date applied, status, and follow-up date.

## Why it matters

The exposure itself is mild — this is product instruction text, not credentials or user data. The
distribution surface is the real issue. A URL is the single leakiest place to put anything:

- Written to browser history and synced across a user's devices
- Emitted in `Referer` headers to third-party origins on subsequent navigation
- Captured by analytics, CDN access logs, and corporate proxies in plaintext
- Preserved verbatim whenever a user copies or shares the link
- Interpolates a user-supplied profile URL into the payload, so the parameter also carries
  personally identifying data into every one of the above

It also means the workflow's scope is fully legible to anyone evaluating whether to pay for it —
which, depending on your view, is either a leak or accidental marketing.

## Recommendation

- Replace the inline `qfill` payload with a short server-side template identifier
  (`?tmpl=job-pipeline`), resolving the prompt after the redirect.
- Keep user-supplied values (profile URLs) out of query strings entirely; carry them in session
  state or a POST body.
- If the parameter must persist, strip it before it reaches analytics and set
  `Referrer-Policy: strict-origin-when-cross-origin` on the surface.
