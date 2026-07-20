# Controller revision 7 open request

| Field | Value |
| --- | --- |
| ID | `REF-CONTROLLER-OPEN-V7` |
| Status | Accepted |
| Product | `PROD-PARCEL-PICKUP` |
| Product authority scope | Locker custody safety |
| Accepted change | `CHG-20260701-CONTROLLER-UNCERTAINTY` |
| Governing intent IDs | `CAP-PICKUP.start-open-request`, `CAP-PICKUP.one-request-id`, `PROD-PARCEL-PICKUP.secret-boundary` |
| Source path | `intent/references/controller-open-v7.json` |
| Reviewable rendering or export | Same as source |
| Format | JSON |
| Last reviewed | 2026-07-20 |

## Why this medium belongs at the product boundary

The Parcel Pickup Coordinator and a revision 7 locker controller must exchange
the same field names and value meanings. A checked-in JSON request shows the
wire shape more clearly than repeating it in several scenarios.

## Normative scope

The artifact requires:

- one top-level JSON object with exactly the four shown fields;
- the literal `open_compartment` as `type`;
- a non-empty string logical open request ID as `request_id`;
- a non-empty string assigned site ID as `site_id`; and
- a non-empty string assigned compartment ID as `compartment_id`.

The artifact illustrates but does not require:

- the sample values for request, site, and compartment;
- field order, indentation, and line endings; and
- any transport envelope or controller authentication outside the JSON body.

## Allowed variation

| Condition | Implementations may vary | Implementations must preserve |
| --- | --- | --- |
| Every revision 7 open request | Real identifier values, JSON field order, and whitespace | The four field names, `open_compartment` type, field meanings, and absence of extra body fields |

## Semantic contract

`CAP-PICKUP.start-open-request` defines when the product sends the request and
which assignment it names. `CAP-PICKUP.one-request-id` defines reuse across
retries. `PROD-PARCEL-PICKUP.secret-boundary` forbids the pickup token. The
fixture does not add actors, permissions, timing, retry, or state duties.

## Acceptance

| Governing intent ID | Comparison conditions | Evidence needed |
| --- | --- | --- |
| `CAP-PICKUP.start-open-request` | Controller contract revision 7 | Capture every first attempt and compare its parsed body with the governed fields and meanings |
| `CAP-PICKUP.one-request-id` | First attempt and every retry for one logical request | Compare each captured `request_id` with the first attempt |
| `PROD-PARCEL-PICKUP.secret-boundary` | Valid, invalid, and repeated pickup-token paths | Inspect captured request bodies for token, recipient, and parcel fields or values |
