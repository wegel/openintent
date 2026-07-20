# Courier expired-stop card hierarchy

| Field | Value |
| --- | --- |
| ID | `REF-COURIER-STOP-CARD` |
| Status | Draft |
| Product | `PROD-COURIER-CONSOLE` |
| Product authority scope | Courier exception work; courier data access |
| Accepted change | Pending |
| Governing intent IDs | `CAP-COURIER-EXCEPTIONS.show-assigned-stop`, `CAP-COURIER-EXCEPTIONS.record-removal` |
| Source path | `products/courier-console/intent/references/expired-stop-card.svg` |
| Reviewable rendering or export | Same as source |
| Format | SVG |
| Last reviewed | 2026-07-20 |

## Why this medium belongs at the product boundary

A courier must distinguish the stop location from the result's synchronization
state at a glance. Side-by-side phone and desktop drawings communicate the
required visual grouping and reading order more clearly than duplicated prose.

## Normative scope

The artifact requires:

- a pending result's synchronization state appears before the stop location;
- the site and compartment form one visual group;
- assignment age appears after that location group; and
- a pending removal result keeps its synchronization label next to the result.

The artifact illustrates but does not require:

- the sample site, compartment, age, and result values;
- the illustrated network-state label;
- exact frame size, spacing, font, line weight, color, corner radius, or icon;
- the surrounding application shell and navigation; and
- the exact phone or desktop platform.

## Allowed variation

| Condition | Implementations may vary | Implementations must preserve |
| --- | --- | --- |
| Phone target | Width, wrapping, touch control size, platform type style, and vertical spacing | Pending synchronization state first, grouped location, age after location, and result with adjacent synchronization state |
| Desktop target | Width, density, pointer control size, platform type style, and horizontal spacing | Pending synchronization state first, grouped location, age after location, and result with adjacent synchronization state |
| Localization or large text | Line breaks, card height, and control placement | Reading order, semantic labels, complete values, and the four governed relationships |

## Semantic contract

`CAP-COURIER-EXCEPTIONS.show-assigned-stop` defines which stop fields the
product shows and who may see them. `CAP-COURIER-EXCEPTIONS.record-removal`
defines the pending result and its meaning. This reference supplies only the
declared visual relationships. It does not define permissions, result states,
platform support, interaction behavior, or accessible names.

## Acceptance

| Governing intent ID | Comparison conditions | Evidence needed |
| --- | --- | --- |
| `CAP-COURIER-EXCEPTIONS.show-assigned-stop` | Phone and desktop target at default and large text sizes | Render comparison for location grouping and assignment-age order plus accessibility-tree reading order |
| `CAP-COURIER-EXCEPTIONS.record-removal` | Pending offline result on phone and desktop | Render and accessibility-tree comparison that places pending synchronization state before location and keeps it adjacent to the result where the result appears |
