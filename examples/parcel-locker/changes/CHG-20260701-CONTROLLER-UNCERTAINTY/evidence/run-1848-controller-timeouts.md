# Fictional run 1848: controller timeouts and recovery

This file illustrates a test report. No executable harness ships with the
OpenIntent repository.

| Field | Value |
| --- | --- |
| Implementation target | `IMPL-PICKUP-SERVICE` |
| Intent revision | `intent-example-17` |
| Build | `example-build-17` |
| Harness | Parcel harness 2.3 |
| Controller | Simulator 3.2, contract revision 7 |
| Started | 2026-07-10T15:18:44Z |
| Requirement tags | `CAP-PICKUP.unknown-result-blocks-claim`, `CAP-PICKUP.one-request-id`, `CAP-PICKUP.start-open-request.claim-to-first-attempt`, `CAP-PICKUP.retry-unknown-result.lost-success`, `CAP-PICKUP.exhaustion-requires-recovery.controller-unreachable`, `CAP-PICKUP.apply-definite-open-result.executed-and-not-executed`, `CAP-PICKUP.reconcile-unknown-result`, `CAP-PICKUP.reconcile-unknown-result.late-success`, `CAP-PICKUP.reconcile-unknown-result.safe-release` |

## Cases

### All results lost

The harness created 500 valid claims. The simulator dropped all three attempt
results. A second submission tried to claim each assignment after attempt three.

| Measure | Expected | Observed |
| --- | --- | --- |
| Total attempts per logical request | At most 3 | 3 for all 500 |
| Distinct request IDs per logical request | 1 | 1 for all 500 |
| Time from first attempt to `Recovery required` | At most 25 seconds | Maximum 20.8 seconds |
| Claims retained | 500 | 500 |
| New claims granted while result unknown | 0 | 0 |
| Recipient operator-help results | 500 | 500 |

### First success response lost

For 500 more claims, the controller executed attempt one and dropped its
response. Attempt two repeated the request ID and received the retained success.

| Measure | Expected | Observed |
| --- | --- | --- |
| Physical open actions | 500 | 500 |
| Controller transmissions | 1,000 | 1,000 |
| Assignments in `Collecting` | 500 | 500 |
| New logical requests after timeout | 0 | 0 |

### Reconciliation matrix

| Controller result | Window | Door | Expected state | Observed state |
| --- | --- | --- | --- | --- |
| Executed | Open | Open | `Collecting` | `Collecting` |
| Not executed | Open | Closed | `Available` | `Available` |
| Not executed | Ended | Closed | `Expired` | `Expired` |
| Unknown | Open | Closed | `Recovery required` | `Recovery required` |
| Not found after reboot | Open | Closed | `Recovery required` | `Recovery required` |
| Executed | Open | Conflicting sensor result | `Recovery required` | `Recovery required` |

Every executed reconciliation retained the original claim and open request ID.
Every safe non-execution result ended the claim. No unknown result released an
assignment.

## Attempt timing

Across 1,000 timed logical requests:

- maximum claim-to-first-attempt time: 1.31 seconds;
- maximum first-to-final-attempt window: 19.74 seconds;
- request ID mismatches: 0; and
- attempts sent after a definite result: 0.

## Result

PASS for `CAP-PICKUP.unknown-result-blocks-claim`,
`CAP-PICKUP.one-request-id`, `CAP-PICKUP.start-open-request`,
`CAP-PICKUP.retry-unknown-result`,
`CAP-PICKUP.exhaustion-requires-recovery`,
`CAP-PICKUP.apply-definite-open-result`, and
`CAP-PICKUP.reconcile-unknown-result`, including every scenario named in the
requirement tags.

## Limits

- The simulator follows its declared duplicate-ID contract and may not reproduce
  a firmware defect.
- A reboot returns `not found`; the run proves only that the product remains in
  recovery, not whether the physical door opened.
- Network timing remained inside the harness profile.
