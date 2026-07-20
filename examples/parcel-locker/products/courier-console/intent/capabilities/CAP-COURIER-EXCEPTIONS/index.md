# Resolve courier exception stops

| Field | Value |
| --- | --- |
| ID | `CAP-COURIER-EXCEPTIONS` |
| Status | Draft |
| Product authority scope | Courier exception work; courier data access |
| Accepted change | Pending |
| Last reviewed | 2026-07-20 |
| Read with | `products/courier-console/intent/product.md`, `products/courier-console/intent/references/REF-COURIER-STOP-CARD.md`, `intent/product.md`, `intent/capabilities/CAP-PICKUP.md` |

## Outcome and boundary

An authorized courier can resolve an assigned expired-parcel stop. This
capability begins when the fulfillment system assigns a removal stop and ends
when that system accepts or rejects the courier's result. The fulfillment
system owns the durable removal work record.

## Content map

| Topic | Path | Owned intent IDs | Read with | Triggers |
| --- | --- | --- | --- | --- |
| Expired-parcel stops | `expired-parcels.md` | `CAP-COURIER-EXCEPTIONS.show-assigned-stop`, `CAP-COURIER-EXCEPTIONS.record-removal`, `CAP-COURIER-EXCEPTIONS.sync-one-result` and their scenarios | `products/courier-console/intent/product.md`, `products/courier-console/intent/references/REF-COURIER-STOP-CARD.md`, `intent/product.md`, `intent/capabilities/CAP-PICKUP.md` | expired, route, removal, offline, synchronize |

## Capability-wide actors and invariants

### CAP-COURIER-EXCEPTIONS.one-logical-result One logical result

The Courier Console MUST use one result ID when it retries the same locally
recorded removal result.

## Capability-wide acceptance map

| Intent ID | Evidence needed |
| --- | --- |
| `CAP-COURIER-EXCEPTIONS.one-logical-result` | Disconnect and reconnect during transfer, then compare local and fulfillment result IDs |

## Open questions

- **OPEN QUESTION:** Which accepted interface supplies expired-parcel stops and
  their freshness state? Owner: Nia Morgan. Blocks: all capability IDs.
- **OPEN QUESTION:** Which phone platform and desktop platform define each
  target's first supported scope? Owner: Nia Morgan. Blocks: target scope and
  platform-specific variation review for `REF-COURIER-STOP-CARD`.
