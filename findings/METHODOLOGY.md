# How I looked, and the guess that was wrong

## Tooling

Read-only the whole way: accessibility-tree reads, page-text extraction, and screenshots at a few
zoom levels and window sizes. I didn't replay any requests, didn't log in, didn't probe rate
limits, and didn't touch anything server-side beyond loading a public page.

## The guess that was wrong

I'll write this down because it's the same guess most "paywall bypass" posts start from.

**Guess:** the panel is hiding report content that's already in the browser, and if I collapse or
move it, that content will show up.

**Test:** edited the panel's CSS in devtools, resized to a narrow portrait window, and dropped to
50% zoom. The panel did move — that's [F-03](F-03-overlay-detaches.md).

**Result:** it revealed nothing. Two checks explain why:

1. **The list is already complete.** The accessibility tree — including non-visible nodes — returns
   exactly five `listitem`s in every state I looked at. No hidden sixth card, nothing truncated.
   The five cards were never concealed; the blur over them is the modal's backdrop, not a lock.
2. **The paid feature isn't in the browser.** The "full workflow" is four nodes of copy plus a link
   to checkout. It's generated server-side after payment, so there's no markup to un-hide.

The thing that *looked* like proof of my guess — "7 identified" over five cards — was just
[F-01](F-01-count-inconsistency.md), a display bug.

## Why the dead end is worth keeping

You can't retrieve bytes the server didn't send by rearranging a page. A write-up claiming
otherwise here would be undone by anyone who opened devtools for thirty seconds. The four things
actually worth reporting all turned up on the way to that, and none of them needed defeating
anything.
