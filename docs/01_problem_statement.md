# 01. Problem Statement

## Background

Myntra's visual search, powered by ViSenze, lets users upload or screenshot a photo instead of typing keywords to find products. It's a genuine success: image-search traffic has grown 35% year-over-year, and the "View Similar" and "Shop the Look" carousels built on the same technology drive meaningful conversion, especially for Gen Z users who shop by "See, Search, Shop" rather than by keyword.

## The gap

The current flow treats the **entire uploaded photo as a single query**. This works well when the photo is a clean, single-product shot (e.g. a product listing screenshot). It breaks down for the photo type that's most common in real usage: an **outfit or lifestyle photo containing multiple garments** — a friend wearing a jacket, jeans, and sneakers; an influencer's Instagram photo; a screenshot from Pinterest.

In this scenario, the user usually wants **one specific item** ("that jacket"), but the system has no way to know which one — so it either:
- Returns a blended set of results skewed toward the most visually dominant item in the frame (often not what the user meant), or
- Returns generic "similar style" results across the whole image, diluting relevance.

## Who this affects

- Any user searching from a photo that isn't a clean single-product shot — which, based on how people actually discover fashion (influencers, friends, street style, Pinterest), is a large and growing share of visual search sessions as image-search adoption keeps climbing.
- Disproportionately affects the **exact use case Myntra is optimizing for**: Gen Z users drawing inspiration from photos "in the wild," not from Myntra's own clean catalog images.

## Why it costs the business

- **Lower search-to-cart conversion** on multi-item photos specifically, since the top results don't match intent.
- **Increased re-search / abandonment**: a user who doesn't find the right item after one attempt is more likely to give up than to manually crop and retry (most users don't know a crop option is even possible unless it's surfaced).
- **Missed multi-item basket opportunity**: if the user wanted the jacket but would also have bought the jeans if easily searchable, that second sale is lost entirely because there's no mechanism to search a second item from the same photo.

## Problem statement (one line)

> Myntra's visual search cannot resolve user intent when a photo contains multiple garments, causing irrelevant results, lost conversions, and missed multi-item purchase opportunities — despite this being an increasingly common real-world search input.
