# Myntra Visual Search: Tap-to-Select for Multi-Item Photos

**A Product Management Case Study**
Sambhavya Nayak | Sumiran Kumar

## TL;DR

Myntra's visual search (powered by ViSenze) already lets users search by photo, and image-search traffic has grown 35% YoY. But it treats each uploaded photo as a single query — so a photo containing multiple garments (e.g. an outfit photo with a jacket, jeans, and bag) returns a blended, ambiguous result set instead of letting the user pick exactly what they want.

This case study proposes **tap-to-select visual search**: auto-detecting individual garments in a photo, letting the user tap the one they want, then refining results with attribute chips (color, price, fabric) — a pattern already proven at scale by Pinterest Lens, adapted here for fashion-specific needs like size, fit, and "shop the whole look" multi-add-to-cart.

## Contents

| Doc | What's inside |
|---|---|
| [01 – Problem Statement](./docs/01_problem_statement.md) | The gap, who it affects, why it costs conversions |
| [02 – Competitive Teardown](./docs/02_competitive_teardown.md) | How Myntra, Pinterest, Amazon, and ASOS currently handle this |
| [03 – Prioritization (RICE)](./docs/03_prioritization_rice.md) | 3 candidate solutions scored and compared |
| [04 – PRD](./docs/04_prd.md) | Full product requirements for the chosen solution |
| [05 – Wireframe Specs](./docs/05_wireframe_specs.md) | Screen-by-screen build spec (for Figma) |
| [06 – Rollout & Measurement Plan](./docs/06_rollout_measurement_plan.md) | A/B test design, success metrics, phased rollout |

## Frameworks used

- **RICE** (Reach, Impact, Confidence, Effort) for prioritization
- **PRD** (Problem → Goal → User Stories → Scope → Metrics) for the spec
- **North Star + Guardrail metrics** for measurement
- **A/B testing** for validation before full rollout
