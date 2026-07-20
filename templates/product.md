# <Product name>

| Field | Value |
| --- | --- |
| ID | `PROD-<NAME>` |
| Status | Draft |
| Product authority scope | `<registry scope>` |
| Accepted change | `<change ID or pending>` |
| Last reviewed | `<YYYY-MM-DD>` |

## Purpose

<!-- State whose problem the product solves and why the product exists. -->

<Concrete purpose>

## Product outcomes

<!-- Name actor-visible results. Do not list components or implementation work. -->

- `<Actor>` can `<outcome>` so that `<real-world result>`.

## Actors

| Actor | Description | Product relationship |
| --- | --- | --- |
| `<actor>` | `<who or what this is>` | `<what the actor needs or controls>` |

## Boundary

The product owns:

- `<outcome or responsibility>`

The following actors or systems own:

- `<external actor or system>` owns `<outside responsibility>`.

## Non-goals

- **NON-GOAL:** `<plausible nearby outcome that this product does not provide>`

## Product invariants

<!-- Keep only rules that constrain every or several capabilities. Put local
invariants in their owning capability. -->

### PROD-<NAME>.<invariant-slug> <Invariant title>

The `<concrete product actor>` MUST `<condition that remains true>`.

## Capability map

| Capability | Outcome | Primary actors | Contract |
| --- | --- | --- | --- |
| `CAP-<NAME>` | `<outcome>` | `<actors>` | `intent/capabilities/CAP-<NAME>.md` |

## Product-wide qualities

<!-- Delete until a cross-cutting quality exists. -->

- [`QLT-<NAME>`](qualities/QLT-<NAME>.md) applies to `<capabilities and reason>`.

## Assumptions and dependencies

- **ASSUMPTION:** `<fact outside product control>`
- `<External system>` provides `<named dependency>` under `<linked contract>`.

## Owned and consumed cross-product contracts

<!-- Delete when this repository contains one product and no outside product
contract needs a durable ownership link. Do not copy another product's rules. -->

| Direction | Product | Boundary | Governing intent IDs | Compatibility or failure behavior |
| --- | --- | --- | --- | --- |
| Owns or consumes | `PROD-<NAME>` | `<shared protocol, data, user, or operator boundary>` | `<owner's IDs>` | `<what this product promises when the boundary changes or fails>` |

## Acceptance map

| Intent ID | Evidence needed |
| --- | --- |
| `PROD-<NAME>.<invariant-slug>` | `<cross-capability or boundary check that could disprove the invariant>` |

## Open questions

<!-- Accepted product intent cannot keep a question that blocks predictable
conformance. Move active questions to the change record and delete this section
before acceptance. -->

- **OPEN QUESTION:** `<question>` Owner: `<person>`. Needed by: `<date or gate>`.
