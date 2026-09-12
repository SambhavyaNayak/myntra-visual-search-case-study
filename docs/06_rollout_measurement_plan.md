# 06. Rollout & Measurement Plan

## Validation approach: A/B Test

Before full rollout, run a controlled experiment rather than shipping directly to everyone.

- **Control group:** existing visual search (whole-photo query, no tap-to-select).
- **Treatment group:** new tap-to-select flow (detection markers, manual crop fallback, refinement chips).
- **Randomization unit:** user, not session — to avoid a single user seeing an inconsistent experience across repeat visits during the test window.
- **Duration:** minimum 2-3 weeks, or until the sample size needed for statistical power is reached (based on baseline visual-search-to-cart conversion rate and the minimum detectable effect the team cares about) — whichever is longer, so the test isn't stopped early on noise.

## Guardrail check before trusting results

As with the Cookie Cats analysis, check for **Sample Ratio Mismatch (SRM)** between control and treatment before drawing any conclusion — confirms the split wasn't corrupted by a logging or targeting bug.

## Primary metric

**Visual-search-to-cart conversion rate**, isolated to sessions where multiple objects were detected in the uploaded photo (this isolates the metric to the exact population the feature targets, rather than diluting it with single-item-photo sessions where nothing changed).

## Secondary metrics

- Re-search rate within a session (searching a 2nd/3rd item from the same photo) — a rise here is expected and healthy.
- Time-to-first-relevant-result (proxy: time from upload to first product-card tap).

## Guardrail metrics (must not regress)

- Search latency (time from upload to first result shown) — object detection adds a processing step; if this regresses meaningfully, it could hurt overall search usage even if relevance improves.
- Single-item-photo search conversion — should be unaffected, since the flow skips the extra tap step when only one item is detected (per the PRD edge case).
- Overall app crash rate / error rate on the search screen (new UI layer = new surface area for bugs).

## Phased rollout (if the A/B test succeeds)

1. **Phase 1:** iOS only, 10% of users — validate stability and detection quality before wider exposure.
2. **Phase 2:** iOS 100%, Android 10% — Android often has more device fragmentation, so a cautious ramp reduces risk of a bad experience on lower-end devices.
3. **Phase 3:** Full rollout on both platforms, with detection model monitoring dashboards kept live post-launch to catch quality drift (e.g. if detection accuracy degrades on certain garment categories over time).

## What "success" looks like at each stage

- **A/B test:** statistically significant lift in the primary metric, no meaningful regression on guardrails.
- **Phase 1-2:** detection latency and crash rate stay within target thresholds at scale.
- **Phase 3:** sustained lift in visual-search-to-cart conversion holds over a full quarter (not just a launch-week novelty effect).
