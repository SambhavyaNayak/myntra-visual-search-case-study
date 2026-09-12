# 03. Prioritization — RICE Framework

## What is RICE?

RICE scores a solution on four factors to make prioritization objective instead of based on whoever argues loudest:

- **Reach** — how many users does this touch in a given period?
- **Impact** — how much does it move the needle per user, on a scale (usually 0.25 = minimal, 0.5 = low, 1 = medium, 2 = high, 3 = massive)?
- **Confidence** — how sure are we of the Reach/Impact estimates (as a %)?
- **Effort** — how many person-months to build?

**RICE Score = (Reach × Impact × Confidence) / Effort** — higher is better.

*Note: since this is a case study without access to Myntra's real traffic data, the numbers below are reasonable estimates used to demonstrate the methodology and the reasoning behind them — not actual company figures.*

## Candidate solutions

### Option A: Tap-to-Select (auto object detection + tap + refine)
Detect multiple garments automatically, highlight them, let the user tap one to search, then refine with attribute chips.

- **Reach:** ~2M visual searches/quarter are estimated to involve multi-item photos (assuming a meaningful minority of the 35%-YoY-growing visual search base).
- **Impact:** 2 (High) — directly resolves the core ambiguity causing irrelevant results.
- **Confidence:** 70% — pattern proven externally (Pinterest) but untested on Myntra's catalog/UX.
- **Effort:** 4 person-months (ML detection model integration/tuning + new UI layer + refinement chips).
- **RICE Score:** (2,000,000 × 2 × 0.7) / 4 = **700,000**

### Option B: Manual Crop Tool Only
Let users manually draw a crop box before searching — no auto-detection, simpler engineering lift.

- **Reach:** ~2M (same affected population), but real-world usage will be lower since manual cropping requires the user to know the feature exists and bother using it.
- **Impact:** 1 (Medium) — solves the problem for users who use it, but adoption will be weak without prompting.
- **Confidence:** 80% — simple, low-risk to estimate.
- **Effort:** 1.5 person-months (UI-only, no ML work).
- **RICE Score:** (2,000,000 × 1 × 0.8) / 1.5 = **1,066,667**

### Option C: Post-Search Attribute Filters Only
Keep search as-is (whole photo), but add filter chips (color, price, fabric) to refine after the fact.

- **Reach:** ~5M (applies to all visual searches, not just multi-item ones).
- **Impact:** 0.5 (Low) — doesn't fix the core relevance problem when multiple items are detected; only helps narrow an already-blended result set.
- **Confidence:** 85% — very low technical risk.
- **Effort:** 1 person-month.
- **RICE Score:** (5,000,000 × 0.5 × 0.85) / 1 = **2,125,000**

## Decision

Ranked by raw RICE score, Option C scores highest — but RICE scores alone can mislead when Impact is scored low for a reason that matters: **Option C doesn't solve the actual problem**, it only polishes results around it. This is a case where a PM should look past the raw score and weigh it against the problem statement.

**Chosen: Option A (Tap-to-Select)**, with **Option C's attribute chips folded in as a refinement step after selection** — combining the highest-impact fix with the cheapest complementary improvement. Option B (crop-only) is deprioritized as a *fallback interaction* within Option A rather than a standalone release: when auto-detection has low confidence or misses an item, the same manual crop tool becomes a safety net inside the tap-to-select flow, not a separate roadmap item.

This is reflected in the PRD (`04_prd.md`), which scopes the full tap-to-select experience with manual crop as a fallback state and attribute chips as post-selection refinement.
