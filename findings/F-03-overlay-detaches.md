# F-03 — Upgrade panel detaches and clips at non-default zoom

**Severity:** Low (responsive layout)
**Status:** Reproducible

## Summary

The upgrade panel is positioned relative to the viewport rather than constrained to its content
container. Below roughly 75% zoom, or in a narrow portrait window, it detaches from its intended
anchor at the foot of the list, migrates toward the top of the viewport, and clips against the
upper edge.

## Repro

1. Open the report page at default zoom on desktop — panel sits centered over the lower list.
2. Resize the window to a narrow portrait aspect ratio.
3. Set zoom to 50%.
4. Panel renders at the **top** of the viewport, its upper portion cut off, overlapping the
   heading region instead of the list.

Captured in `evidence/` at both 100% and 50%.

## Expected

The panel remains anchored to its container and fully visible across the supported zoom range.

## Recommendation

- Constrain positioning to the report container rather than the viewport.
- Add `max-height` with internal scroll so the panel degrades gracefully rather than clipping.
- Test the surface at 50%–200% zoom and at widths below 480 CSS pixels. WCAG 2.1 SC 1.4.4
  (Resize Text) and 1.4.10 (Reflow) are the relevant bars.
