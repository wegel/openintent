# Courier Console intent index

| Field | Value |
| --- | --- |
| Product | Courier Console |
| Product ID | `PROD-COURIER-CONSOLE` |
| Repository index | `../../../intent/index.md` |
| OpenIntent version | `0.1` |
| Accepted branch | `main` |
| Contract state | Draft |
| Last reviewed | 2026-07-20 |

This file routes Courier Console work. It does not restate requirements.

## Product authority registry

| Scope | Authority | May delegate | Conflict resolver | Acceptance record |
| --- | --- | --- | --- | --- |
| Courier exception work | Courier Operations Product Owner, exercised by Nia Morgan | May delegate named IDs in a change record | Nia Morgan | Pending change approval record |
| Courier data access | Courier Security Owner, exercised by Luis Ortega | May delegate evidence review but not product choices | Luis Ortega | Pending change approval record |

## Product

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Read with | Triggers |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `PROD-COURIER-CONSOLE` | Courier Console | Draft | `products/courier-console/intent/product.md` | Courier exception work; courier data access | `IMPL-COURIER-PHONE`, `IMPL-COURIER-DESKTOP` | `intent/product.md`, `intent/capabilities/CAP-PICKUP.md` | courier, expired parcel, route stop, removal |

## Capabilities

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Read with | Triggers |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `CAP-COURIER-EXCEPTIONS` | Resolve courier exception stops | Draft | `products/courier-console/intent/capabilities/CAP-COURIER-EXCEPTIONS/index.md` | Courier exception work; courier data access | `IMPL-COURIER-PHONE`, `IMPL-COURIER-DESKTOP` | `products/courier-console/intent/product.md`, `intent/product.md`, `intent/capabilities/CAP-PICKUP.md` | expired, removal, offline, route, confirmation |

## Normative supporting artifacts

| ID | Title | Intent state | Record | Source | Authority scope | Governing intent IDs |
| --- | --- | --- | --- | --- | --- | --- |
| `REF-COURIER-STOP-CARD` | Courier expired-stop card hierarchy | Draft | `products/courier-console/intent/references/REF-COURIER-STOP-CARD.md` | `products/courier-console/intent/references/expired-stop-card.svg` | Courier exception work; courier data access | `CAP-COURIER-EXCEPTIONS.show-assigned-stop`, `CAP-COURIER-EXCEPTIONS.record-removal` |

## Consumed cross-product contracts

| Contract | Owning product | Governing intent IDs | Local use | Unresolved boundary |
| --- | --- | --- | --- | --- |
| Expired assignment status and data boundary | `PROD-PARCEL-PICKUP` | `PROD-PARCEL-PICKUP.secret-boundary`, `PROD-PARCEL-PICKUP.actor-scope`, `CAP-PICKUP.expire-unclaimed-assignment` | Interpret an assignment as expired without exposing pickup secrets or crossing actor scope | The products have not accepted an interface, freshness promise, or field set |

## Implementation targets

| ID | Kind | Name and scope | Owner | Relationships | Current revision | Accepted intent revision | Checkpoint | Latest evidence |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `IMPL-COURIER-PHONE` | Component | Proposed courier phone app | Courier Mobile team | Consumes the Parcel Pickup Coordinator's expired-status contract and a fulfillment work feed | Not started | None; intent is Draft | Unknown | None |
| `IMPL-COURIER-DESKTOP` | Component | Proposed courier desktop app for shared operations workstations | Courier Desktop team | Consumes the Parcel Pickup Coordinator's expired-status contract and a fulfillment work feed | Not started | None; intent is Draft | Unknown | None |

## Active changes

None. Product authority must create a change record before accepting or
implementing this draft.

## Known conformance gaps

The two Courier Console targets have no implementation revision or accepted
intent revision. Their checkpoints remain `Unknown` by definition.

## ID convention

This product uses `PROD-COURIER-CONSOLE`, `CAP-COURIER-EXCEPTIONS`, and semantic
child IDs. It does not reuse the Parcel Pickup Coordinator's IDs for local
duties.
