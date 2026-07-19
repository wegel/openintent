# Parcel Pickup Coordinator

| Field | Value |
| --- | --- |
| ID | `PROD-PARCEL-PICKUP` |
| Status | Accepted |
| Product authority scope | Parcel pickup behavior; pickup data security and audit |
| Accepted change | `CHG-20260701-CONTROLLER-UNCERTAINTY` |
| Last reviewed | 2026-07-19 |

## Purpose

The Parcel Pickup Coordinator lets a recipient collect one assigned parcel from
a shared locker without exposing recipient identity at the locker. It keeps the
parcel assignment safe when the locker controller returns a late, missing, or
conflicting result.

## Product outcomes

- A recipient with a valid pickup token can open the assigned compartment and
  finish one pickup session.
- A site operator can recover a pickup when hardware results remain unknown.
- An auditor can reconstruct product state changes without seeing pickup tokens.

## Actors

| Actor | Description | Product relationship |
| --- | --- | --- |
| Recipient | Person who possesses a bearer pickup token | Claims and collects the assigned parcel |
| Fulfillment system | Outside service that registers a placed parcel and its pickup window | Creates the assignment before this product takes ownership |
| Locker controller | Outside hardware service that accepts compartment commands and reports door events | Executes a named open request and reports results |
| Site operator | Person with the Site Recovery role for one locker site | Resolves unknown hardware outcomes |
| Auditor | Person with read-only audit permission for an operating region | Reviews state changes and recovery actions |

## Boundary

The product owns:

- pickup claim arbitration;
- open request identity and retry policy;
- pickup state from available through collected, expired, or recovery required;
- actor-visible pickup and recovery results; and
- audit events for pickup state changes.

The following systems own:

- The fulfillment system owns parcel placement, recipient contact, token
  delivery, and removal of parcels that expire.
- The locker controller owns electrical lock actuation, door sensing, and its
  duplicate-request response.

## Non-goals

- **NON-GOAL:** The product does not select a locker or compartment.
- **NON-GOAL:** The product does not prove that the recipient physically removed
  the parcel after the door opened.
- **NON-GOAL:** The product does not route couriers or notify recipients that a
  parcel first became available.

## Product invariants

### PROD-PARCEL-PICKUP.secret-boundary Secret boundary

The Parcel Pickup Coordinator MUST NOT place a raw pickup token in an audit
event, operator view, controller request, or actor-visible error.

### PROD-PARCEL-PICKUP.actor-scope Site scope

The Parcel Pickup Coordinator MUST NOT let a site operator or auditor act on or
read an assignment outside that actor's authorized site or region.

### PROD-PARCEL-PICKUP.audit-read-only Auditors cannot change pickup state

The Parcel Pickup Coordinator MUST NOT let an auditor create a claim, request
controller reconciliation, or change an assignment.

## Acceptance map

| Intent ID | Evidence needed |
| --- | --- |
| `PROD-PARCEL-PICKUP.secret-boundary` | Field inspection of recipient, operator, controller, error, and audit surfaces with a known raw token |
| `PROD-PARCEL-PICKUP.actor-scope` | Positive and negative site and region checks for operators and auditors |
| `PROD-PARCEL-PICKUP.audit-read-only` | Attempts by an authorized auditor to claim, reconcile, and mutate an in-region assignment |

## Capability map

| Capability | Outcome | Primary actors | Contract |
| --- | --- | --- | --- |
| `CAP-PICKUP` | Claim, open, collect, or recover one assigned parcel | Recipient, site operator, locker controller | `intent/capabilities/CAP-PICKUP.md` |

## Product-wide qualities

- [`QLT-AUDIT`](qualities/QLT-AUDIT.md) constrains every pickup state change and
  operator recovery action.

## Assumptions and dependencies

- **ASSUMPTION:** The fulfillment system registers an assignment only after a
  parcel occupies its named compartment.
- **ASSUMPTION:** The locker controller retains an open request result for 24
  hours and returns the same result when the product repeats the request ID.
- The fulfillment system supplies an assignment ID, site, compartment, pickup
  window, and bearer token through its accepted external contract.
