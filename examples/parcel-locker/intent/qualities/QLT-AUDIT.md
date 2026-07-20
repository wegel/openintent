# Timely, secret-free pickup audit

| Field | Value |
| --- | --- |
| ID | `QLT-AUDIT` |
| Status | Accepted |
| Product authority scope | Pickup data security and audit |
| Accepted change | `CHG-20260701-CONTROLLER-UNCERTAINTY` |
| Applies to | `CAP-PICKUP` |
| Last reviewed | 2026-07-20 |

## Product reason

Site operators and auditors need to reconstruct an unsafe or disputed pickup
without receiving the bearer secret that authorizes another pickup attempt.

## Measurement rules

- **State-changing pickup action** means a claim grant, controller result, pickup
  state transition, or operator reconciliation request.
- **Available to audit search** means an authorized auditor can retrieve the
  event by assignment ID and event time through the regional audit interface.
- **Peak-site profile** means the accepted conditions in
  [`PROF-PEAK-SITE`](../profiles/PROF-PEAK-SITE.md).
- Latency starts when the product accepts the state-changing action and ends
  when audit search can return its event.

## Requirements

### QLT-AUDIT.required-event-content Complete event content

For every state-changing pickup action, the Parcel Pickup Coordinator MUST
create an audit event that identifies the event type, assignment, site, actor
class, actor identifier when authenticated, event time, prior state, resulting
state, and related open request ID when one exists.

The event MUST NOT contain a raw pickup token, recipient contact data, parcel
description, or controller credential.

#### QLT-AUDIT.required-event-content.recipient-claim Recipient claim event

This scenario is normative.

- GIVEN a valid token wins a pickup claim
- WHEN the assignment moves from `Available` to `Opening`
- THEN audit search returns one claim-granted event with assignment, site, prior
  and resulting states, and open request ID
- AND the actor class is `token bearer`
- AND the event contains no raw token or recipient identity

### QLT-AUDIT.event-availability Search availability

Under the peak-site profile, the Parcel Pickup Coordinator MUST make at least
99.9 percent of state-changing pickup events available to audit search within
five seconds and MUST make every accepted event available within 60 seconds.

#### QLT-AUDIT.event-availability.peak-site Peak-site run

This scenario is normative.

- GIVEN the peak-site profile and an available regional audit interface
- WHEN the product accepts state-changing pickup actions for 15 minutes
- THEN at least 99.9 percent of corresponding events appear within five seconds
- AND every corresponding event appears within 60 seconds
- AND no assignment has a missing or duplicate event for one accepted action

### QLT-AUDIT.regional-retention Retention and scope

The Parcel Pickup Coordinator MUST keep audit events searchable for 180 days
after their event time and MUST let an auditor retrieve only events from that
auditor's authorized regions.

#### QLT-AUDIT.regional-retention.regional-boundary Regional boundary

This scenario is normative.

- GIVEN an auditor authorized for Region A and events in Regions A and B
- WHEN the auditor searches by a Region B assignment ID
- THEN the audit interface returns no Region B event or assignment metadata
- AND the same auditor can retrieve the Region A event during its 180-day period

## Assumptions

- **ASSUMPTION:** The identity service supplies stable operator and auditor IDs
  and current site or region scopes.
- **ASSUMPTION:** The audit interface clock and product clock differ by no more
  than one second during a measurement run.

## Unspecified observable behavior

- **UNSPECIFIED:** Implementations may store extra non-secret diagnostic fields
  that authorized auditors can see when regional privacy rules permit them.

## Acceptance map

| Intent ID | Environment and workload | Evidence needed | Review cadence |
| --- | --- | --- | --- |
| `QLT-AUDIT.required-event-content`, `QLT-AUDIT.required-event-content.recipient-claim` | Each event type and operator path | Schema and payload inspection plus one-to-one state-action coverage | Every event-shape change |
| `QLT-AUDIT.event-availability`, `QLT-AUDIT.event-availability.peak-site` | `PROF-PEAK-SITE` | Timed report with actual profile conditions, deviations, raw counts, percentile method, slowest event, and missing-event count | Before a throughput increase, audit-path change, or profile edit |
| `QLT-AUDIT.regional-retention`, `QLT-AUDIT.regional-retention.regional-boundary` | Two-region authorization fixture and aged events | Positive and negative query tests at 179 and 181 days | Every permission or retention change |
