# 05. Wireframe Specs (build these in Figma)

General notes: mobile-first (375×812 frame, iPhone-style), Myntra's existing visual language (pink/magenta accent ~#FF3F6C, white background, clean sans-serif). These are layout specs, not final visuals — boxes/labels are enough.

---

## Screen 1: Detection State (right after upload)

**Purpose:** show the user their photo with detected garments highlighted, before any search runs.

Layout, top to bottom:
1. **Top bar:** back arrow (left), title "Search by Photo" (center), close "X" (right).
2. **Full-width photo** (the uploaded image), roughly 70% of screen height.
3. **Overlay markers** on the photo: 2-4 small circular dots (pulsing/glowing style, use the accent pink) positioned over each detected garment (e.g. one on a jacket, one on jeans, one on a bag). Each dot should look clearly tappable (drop shadow, slight scale-up animation if you want to note it as a micro-interaction).
4. **Caption text below the photo:** "Tap an item to search for it" (gray, small, centered).
5. **Secondary link/button below that:** "Can't find it? Select manually →" (text link style, not a filled button — this is the fallback entry point).

---

## Screen 2: Manual Crop (fallback state)

**Purpose:** shown only if the user taps "Select manually," or if detection found nothing.

Layout:
1. Same top bar as Screen 1.
2. Full-width photo, with a **draggable rectangular crop box** overlaid (show it mid-drag with 4 corner handles, dashed border in accent color).
3. Bottom sheet/button: filled pink button, "Search this area," anchored to the bottom of the screen.
4. If this is the "nothing detected" case specifically, add a thin banner above the photo: "We couldn't auto-detect items — try selecting one manually." (light gray background, small text).

---

## Screen 3: Results with Refinement Chips

**Purpose:** shown after tapping a detected item (or confirming a manual crop).

Layout, top to bottom:
1. **Top bar:** back arrow, title showing what was searched, e.g. "Results for: Jacket."
2. **Small thumbnail strip** directly under the top bar: a cropped preview of just the selected garment (so the user has confidence in what was searched) + a small "Search another item from this photo" pill button next to it (this satisfies PRD user story #4).
3. **Horizontal scrollable filter chips row:** "Price," "Color," "Fabric" (each a rounded pill, tap to expand a bottom-sheet filter — you can just show the collapsed pill row, no need to design the expanded filter panel in detail).
4. **Product grid below:** standard 2-column product card grid (image, brand, price) — reuse Myntra's existing product card style, this doesn't need custom design.

---

## Screen 4 (optional, if time allows): Empty/Low-Relevance State

Only build this if you have spare time — it strengthens the "you thought about edge cases" signal.

Layout:
1. Same top bar/thumbnail strip as Screen 3.
2. Centered illustration placeholder (simple icon is fine) + text: "No exact matches — here are the closest styles we found."
3. Product grid below, same as Screen 3, but with a small "Closest Match" tag on each card.

---

## What to export

Once built, export each frame as PNG (or share the Figma file link directly — Notion embeds Figma links natively too). Save exports into an `images/` folder in this repo as `screen1_detection.png`, `screen2_manual_crop.png`, `screen3_results.png`, `screen4_empty_state.png` (if built), so they can be dropped straight into the compiled case study.
