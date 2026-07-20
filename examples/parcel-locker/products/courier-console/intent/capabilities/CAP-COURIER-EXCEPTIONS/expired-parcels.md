# Expired-parcel stops

| Field | Value |
| --- | --- |
| Capability | `CAP-COURIER-EXCEPTIONS` |
| Topic | Expired-parcel stops |
| Status | Draft |
| Read with | `products/courier-console/intent/capabilities/CAP-COURIER-EXCEPTIONS/index.md`, `products/courier-console/intent/product.md`, `products/courier-console/intent/references/REF-COURIER-STOP-CARD.md`, `intent/product.md`, `intent/capabilities/CAP-PICKUP.md` |

## Topic boundary

This topic owns what the courier sees and records from an assigned expired stop
through an accepted or rejected removal result. The fulfillment system owns
route assignment and the durable removal work record.

## Actors, state, and permissions

| Actor | Allowed action | Forbidden action | Scope | Governing intent IDs |
| --- | --- | --- | --- | --- |
| Courier | View an assigned stop and record its removal result | View another route or any pickup secret | Assigned route stops | `PROD-COURIER-CONSOLE.assigned-work-only`, `PROD-COURIER-CONSOLE.no-pickup-secrets`, `CAP-COURIER-EXCEPTIONS.show-assigned-stop` |
| Courier operations worker | View rejected results and their non-secret reason | Change a courier's local pending result | Assigned region | `PROD-COURIER-CONSOLE.assigned-work-only`, `CAP-COURIER-EXCEPTIONS.sync-one-result` |

## Requirements and normative scenarios

### CAP-COURIER-EXCEPTIONS.show-assigned-stop Show an assigned expired stop

When the fulfillment system assigns an expired-parcel stop to an authenticated
courier, the Courier Console MUST show the site, compartment, route-stop ID,
and assignment age. It MUST NOT show a pickup token, recipient contact data, or
another route's stop. Phone and desktop stop cards MUST preserve the visual
grouping and reading order governed by `REF-COURIER-STOP-CARD` so a courier can
distinguish location and synchronization state. Each target MUST expose the
same labels, values, states, and reading order to its platform accessibility
service.

#### CAP-COURIER-EXCEPTIONS.show-assigned-stop.wrong-route Wrong route stays hidden

This scenario is normative.

- GIVEN one expired-parcel stop on the courier's route and one on another route
- WHEN the courier opens the stop list
- THEN the list shows only the assigned route's stop
- AND no response, screen, or local cache contains the other stop's fields

### CAP-COURIER-EXCEPTIONS.record-removal Record a removal result offline

When a courier records `removed`, `not present`, or `cannot access` for an
assigned stop without a network connection, the Courier Console MUST retain one
pending result with a new result ID and MUST show that it has not synchronized.
The pending result and its synchronization state MUST preserve the visual and
reading-order relationship governed by `REF-COURIER-STOP-CARD`.

#### CAP-COURIER-EXCEPTIONS.record-removal.app-restart Pending result survives restart

This scenario is normative.

- GIVEN a courier records `removed` while the device is offline
- WHEN the app stops and starts before the network returns
- THEN the same pending result and result ID remain visible
- AND the app does not show the result as accepted

### CAP-COURIER-EXCEPTIONS.sync-one-result Synchronize one logical result

When the network returns, the Courier Console MUST send the pending result with
its original result ID until the fulfillment system accepts or rejects it. It
MUST show the accepted or rejected result without creating another logical
result.

#### CAP-COURIER-EXCEPTIONS.sync-one-result.lost-acceptance Lost acceptance response

This scenario is normative.

- GIVEN the fulfillment system accepts a result but its response is lost
- WHEN the Courier Console retries after reconnecting
- THEN the retry carries the original result ID
- AND the fulfillment system's retained acceptance ends the pending state
- AND one logical result remains visible

## Assumptions

- **ASSUMPTION:** The fulfillment system retains accepted result IDs long
  enough for an offline device to retry.

## Topic acceptance map

| Intent ID | Evidence needed |
| --- | --- |
| `CAP-COURIER-EXCEPTIONS.show-assigned-stop`, `CAP-COURIER-EXCEPTIONS.show-assigned-stop.wrong-route` | Positive and negative route fixtures plus screen, response, and cache inspection; compare governed visual and reading-order properties with `REF-COURIER-STOP-CARD` |
| `CAP-COURIER-EXCEPTIONS.record-removal`, `CAP-COURIER-EXCEPTIONS.record-removal.app-restart` | Offline capture followed by a process stop and restart; compare the pending-result relationship with `REF-COURIER-STOP-CARD` |
| `CAP-COURIER-EXCEPTIONS.sync-one-result`, `CAP-COURIER-EXCEPTIONS.sync-one-result.lost-acceptance`, `CAP-COURIER-EXCEPTIONS.one-logical-result` | Lost-response retry with local and fulfillment result counts and IDs |
