# 04. Product Requirements Document (PRD)

## Feature: Tap-to-Select Visual Search

**Owner:** Sambhavya Nayak (case study) | **Status:** Draft for review

## Problem

See [01_problem_statement.md](./01_problem_statement.md). In short: Myntra's visual search can't resolve which garment a user wants when a photo contains multiple items, hurting relevance and conversion.

## Goal

Let users isolate and search for a specific garment within a multi-item photo, then refine results by fashion-relevant attributes — reducing irrelevant results and increasing visual-search-to-cart conversion.

## Non-goals (out of scope for v1)

- Video-based visual search
- Real-time camera "live view" search (search is on a captured/uploaded photo only)
- Multi-item simultaneous search (searching 2+ items at once in a single result view) — v1 is one selection at a time, repeatable
- Style/outfit recommendation generation from the photo (that's the existing "Shop the Look" feature, left untouched)

## User stories

1. **As a user** who uploads a photo with multiple garments, **I want** the app to show me which items it detected, **so that** I can pick the exact one I'm interested in.
2. **As a user**, if the app doesn't detect the item I want (e.g. an accessory, or poor lighting), **I want** to manually draw a selection box, **so that** I'm not blocked by detection failures.
3. **As a user**, after selecting an item, **I want** to filter results by price, color, or fabric, **so that** I can narrow down to something I'd actually buy.
4. **As a user**, after finding and liking a result from one item in the photo, **I want** to easily go back and search a *different* item from the same photo, **so that** I can shop the whole look without re-uploading.

## Flow

1. User uploads/captures a photo (existing entry point, unchanged).
2. **New:** App runs object detection; detected garments are highlighted with tappable markers over the image.
3. User taps a marker → search runs scoped to that region → results load below/beside the image.
4. **Fallback:** if detection finds nothing or the user wants a different region, a "Select manually" option reveals a draggable crop box.
5. Above the results, attribute filter chips appear (Color, Price, Fabric/Material) generated based on the detected item's category.
6. A persistent "Search another item from this photo" affordance lets the user return to step 2's marker view without re-uploading.

## Edge cases

| Case | Behavior |
|---|---|
| No objects detected (e.g. blurry photo, no clear garment) | Show manual crop tool immediately with a short prompt: "We couldn't auto-detect items — try selecting one manually." |
| Only one object detected | Skip the tap step, go straight to results (don't add friction when there's no ambiguity to resolve). |
| Low-confidence detection | Still show the marker, but visually de-emphasized (lower opacity), so the user isn't misled into trusting a bad guess. |
| Selected item has zero catalog matches | Show closest visual matches with a clear "closest matches, not exact" label rather than an empty state. |

## Success metrics

- **Primary (North Star for this feature):** Visual-search-to-cart conversion rate, specifically on sessions involving multi-item photos (detected via the object-detection step firing more than once).
- **Secondary:** 
  - Re-search rate within a visual search session (expected to increase slightly and healthily — searching a second item from the same photo is now easy, whereas before it required a fresh upload).
  - Zero-result / low-relevance-result rate on multi-item photos (expected to decrease).
- **Guardrails (should not regress):**
  - Overall visual search latency (object detection adds a processing step — must stay within acceptable load time, target: no more than +300ms to first result).
  - Single-item photo search conversion (must not regress from the added UI step, since single-item flow should stay just as fast per the "skip the tap step" edge case above).

## Dependencies

- ViSenze (or equivalent) needs to support returning multiple bounding boxes per image, not just a single best-match region — a vendor/infra conversation, not just a UI change.
