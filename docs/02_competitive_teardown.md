# 02. Competitive Teardown

## Myntra (current state)

- Visual search powered by ViSenze's Discovery Suite.
- Supports photo upload, saved images, and screenshots.
- Powers "View Similar" (visually-similar carousel) and "Shop the Look" (pulls multiple items from a single model photo for cross-sell).
- No evidence of a user-facing multi-object selection step — the system appears to process the image as a whole rather than letting the user isolate one garment before searching.

## Pinterest Lens (best-in-class reference)

Pinterest solved this problem years ago and it's worth adopting their proven pattern rather than reinventing it:
- Detected objects in a photo **glow** to indicate they're tappable.
- Tapping a glowing item selects it and searches specifically for that object.
- Users can also **pinch-to-zoom or drag a cropper** for manual, free-form selection when auto-detection misses the item they want.
- Results update dynamically based on which object is selected, with suggested keyword chips to refine further.
- This is backed by real object detection models (Faster R-CNN-style architectures) trained specifically to find multiple distinct objects in one frame — not a gimmick, a core piece of infrastructure.

**Takeaway:** the "glowing dot + tap to select + optional manual crop" pattern is proven at massive scale. Myntra doesn't need to invent a new interaction model — it needs to adopt this one and adapt it for commerce-specific needs (below).

## Amazon Lens / general e-commerce visual search

- Typically supports single-object search with a manual crop tool, but lacks the automatic multi-object detection that Pinterest has — closer to Myntra's current state than to Pinterest's.

## ASOS (via ViSenze, same vendor as Myntra)

- Uses visual similarity primarily for "out of stock alternatives" — recommending visually similar items when a product is unavailable, rather than solving the multi-item-in-one-photo problem directly.

## The opportunity for Myntra

Myntra already has the underlying visual search infrastructure (via ViSenze) that Pinterest-style multi-object detection would plug into. The gap is specifically the **user-facing selection layer** — and fashion adds a dimension competitors don't fully address: once an item is selected, refinement should include **fashion-specific attributes** (size availability, fit type, price band, fabric) rather than just visual similarity, and a **multi-item photo should let a user search and add more than one item from the same photo to their cart in one flow** ("shop the whole look, one tap at a time").
