# Fictional run 1851: permissions and audit

This file illustrates a test report. No executable harness ships with the
OpenIntent repository.

| Field | Value |
| --- | --- |
| Implementation target | `IMPL-PICKUP-SERVICE` |
| Intent revision | `intent-example-17` |
| Build | `example-build-17` |
| Harness | Parcel harness 2.3, regional audit simulator 1.8 implementing contract revision 1 |
| Operating profile | `PROF-PEAK-SITE` at `intent-example-17` |
| Started | 2026-07-11T09:00:00Z |
| Regions | A and B, two sites each |
| Requirement tags | `PROD-PARCEL-PICKUP.secret-boundary`, `PROD-PARCEL-PICKUP.actor-scope`, `PROD-PARCEL-PICKUP.audit-read-only`, `CAP-PICKUP.unavailable-token-disclosure.expired-and-unknown`, `CAP-PICKUP.restrict-operator-recovery.out-of-scope-operator`, `CAP-PICKUP.audit-pickup-actions.recovery`, `QLT-AUDIT.required-event-content`, `QLT-AUDIT.required-event-content.recipient-claim`, `QLT-AUDIT.event-availability.peak-site`, `QLT-AUDIT.regional-retention.regional-boundary` |

## Permission matrix

The harness created a recovery assignment at each site and used operators with
one-site, two-site, and no-site scope.

| Action | Cases | Expected allowed | Observed allowed | Cross-scope fields returned |
| --- | --- | --- | --- | --- |
| Reconcile assigned site | 400 | 400 | 400 | 0 |
| Reconcile other site in same region | 400 | 0 | 0 | 0 |
| Reconcile other region | 400 | 0 | 0 | 0 |
| Mark collected through recovery interface | 400 | 0 | 0 | 0 |
| Read audit in assigned region | 400 | 400 | 400 | 0 |
| Read audit in other region | 400 | 0 | 0 | 0 |
| Auditor claims an in-region assignment | 400 | 0 | 0 | 0 |
| Auditor reconciles an in-region assignment | 400 | 0 | 0 | 0 |
| Auditor mutates an in-region assignment | 400 | 0 | 0 | 0 |

Denied response bodies matched the declared generic denial shape. The harness
found no assignment ID, site, parcel, recipient, token, or controller-result
field in an out-of-scope response.

## Token and secret scan

The harness emitted every pickup and recovery event type, then compared raw and
encoded token values, recipient fixture fields, parcel descriptions, and
controller credentials with declared response, event, and search schemas.

| Scan target | Records | Forbidden matches |
| --- | --- | --- |
| Recipient unavailable responses | 6,000 | 0 |
| Operator recovery responses | 1,200 | 0 |
| Audit outbox events | 10,000 | 0 |
| Search projection events | 10,000 | 0 |

Every state-changing action produced exactly one event with event type,
assignment, site, actor class, event time, prior state, resulting state, and open
request ID where applicable. Authenticated operator events also held the operator
ID. Token-bearer events held no person ID.

## Peak-site profile

The harness accepted 500 state-changing pickup actions per second for 900
seconds, for 450,000 actions. It used two service processes with four workers
each, controller contract revision 7, and the available regional audit
interface. A pre-run search succeeded, the audit backlog counter read zero, and
no assignment supplied more than 5 percent of actions. The run had no deviation
from `PROF-PEAK-SITE`.

| Measure | Required | Observed |
| --- | --- | --- |
| Events accepted | 450,000 | 450,000 |
| Events searchable within 5 seconds | At least 99.9% | 99.973% |
| Slowest 0.1% threshold | At most 5 seconds | 4.62 seconds |
| Maximum search availability | At most 60 seconds | 17.4 seconds |
| Missing events after 60 seconds | 0 | 0 |
| Duplicate events for one action | 0 | 0 |

## Retention boundary

With a controlled clock, the Region A auditor retrieved Region A events at 179
days and could not retrieve them after the 180-day period ended. The same
auditor never retrieved Region B events. The store lifecycle deleted 10,000 of
10,000 expired fixture events.

## Result

PASS for `PROD-PARCEL-PICKUP.secret-boundary`,
`PROD-PARCEL-PICKUP.actor-scope`,
`PROD-PARCEL-PICKUP.audit-read-only`,
`CAP-PICKUP.unavailable-token-disclosure`,
`CAP-PICKUP.restrict-operator-recovery`,
`CAP-PICKUP.audit-pickup-actions`,
`QLT-AUDIT.required-event-content`, `QLT-AUDIT.event-availability`, and
`QLT-AUDIT.regional-retention`, including every scenario named in the
requirement tags.

## Limits

- The identity service and regional store were simulators.
- The secret scan inspected declared response and event schemas, not arbitrary
  debug logs outside the audit path.
- The retention run advanced a controlled clock; it did not operate for 180
  wall-clock days.
