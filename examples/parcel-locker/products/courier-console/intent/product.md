# Courier Console

| Field | Value |
| --- | --- |
| ID | `PROD-COURIER-CONSOLE` |
| Status | Draft |
| Product authority scope | Courier exception work; courier data access |
| Accepted change | Pending |
| Last reviewed | 2026-07-20 |

## Purpose

The Courier Console would let an authorized courier find and resolve assigned
parcel-removal stops after pickup windows expire. It would run on a courier's
phone and on a shared operations desktop without exposing recipient pickup
secrets.

## Product outcomes

- A courier can find expired-parcel stops assigned to that courier's route.
- A courier can record one removal result while offline and send it after the
  device reconnects.
- An operations worker can distinguish pending, synchronized, and rejected
  removal results.

## Actors

| Actor | Description | Product relationship |
| --- | --- | --- |
| Courier | Authenticated worker assigned to one or more route stops | Views assigned stops and records removal results |
| Courier operations worker | Authenticated worker responsible for a region | Reviews unresolved or rejected results in that region |
| Fulfillment system | Outside system that owns expired-parcel removal work | Supplies assignments and accepts removal results |
| Parcel Pickup Coordinator | Separate product that owns pickup status and pickup-data boundaries | Supplies owned status meaning if the products later accept an interface |

## Boundary

The proposed product owns:

- route-stop presentation on phone and desktop;
- offline capture and later transfer of removal results; and
- actor-visible state for pending, synchronized, and rejected results.

The fulfillment system owns route planning, the removal work record, and the
decision to accept or reject a result. The Parcel Pickup Coordinator owns pickup
state and does not grant Courier Console a new interface through this draft.

## Non-goals

- **NON-GOAL:** The Courier Console does not open locker compartments.
- **NON-GOAL:** The Courier Console does not change pickup assignment state.
- **NON-GOAL:** The Courier Console does not show pickup tokens or recipient
  contact data.

## Product invariants

### PROD-COURIER-CONSOLE.assigned-work-only Assigned work only

The Courier Console MUST NOT show or accept a removal result for a route stop
outside the authenticated actor's assigned route or region.

### PROD-COURIER-CONSOLE.no-pickup-secrets No pickup secrets

The Courier Console MUST NOT store or show a pickup token or recipient contact
data.

## Acceptance map

| Intent ID | Evidence needed |
| --- | --- |
| `PROD-COURIER-CONSOLE.assigned-work-only` | Positive and negative route and region checks on phone and desktop surfaces |
| `PROD-COURIER-CONSOLE.no-pickup-secrets` | Field, cache, log, and screen inspection with known pickup and recipient values |

## Capability map

| Capability | Outcome | Primary actors | Contract |
| --- | --- | --- | --- |
| `CAP-COURIER-EXCEPTIONS` | Find expired-parcel stops and record their outcome | Courier; courier operations worker | `products/courier-console/intent/capabilities/CAP-COURIER-EXCEPTIONS/index.md` |

## Assumptions and dependencies

- The proposed product depends on the fulfillment system supplying assigned
  removal stops and accepting one result ID. The products have not accepted
  that interface, field set, or retry period.
- The proposed product depends on the Parcel Pickup Coordinator's owned
  `Expired` meaning and data boundaries. That dependency does not create an
  interface between the products.

## Owned and consumed cross-product contracts

- The Courier Console owns no Parcel Pickup Coordinator rule.
- It consumes the accepted `Expired` meaning, secret boundary, and actor-scope
  rules named in the repository index.
- This draft does not define the transport, fields, update rate, or failure
  behavior between products. Product authority must resolve those points before
  implementation begins.
