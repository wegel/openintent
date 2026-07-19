# Fictional run 1854: door and expiry boundaries

This file illustrates a test report. No executable harness ships with the
OpenIntent repository.

| Field | Value |
| --- | --- |
| Implementation target | `IMPL-PICKUP-SERVICE` |
| Intent revision | `intent-example-17` |
| Build | `example-build-17` |
| Harness | Parcel harness 2.3 with controlled product clock |
| Started | 2026-07-11T12:30:00Z |
| Requirement tags | `CAP-PICKUP.collected-after-open-close`, `CAP-PICKUP.close-completes-pickup.missing-close`, `CAP-PICKUP.expire-unclaimed-assignment.window-end`, `CAP-PICKUP.claim-expiry-race.overlap`, `CAP-PICKUP.reject-unmatched-controller-result.wrong-request` |

## Door-event permutations

The harness ran 100 sessions for each event sequence.

| Sequence | Expected state | Observed sessions |
| --- | --- | --- |
| Close before any confirmed open | `Opening` | 100 of 100 |
| Confirmed open, then close | `Collected` | 100 of 100 |
| Confirmed open, no close for two minutes | `Recovery required` | 100 of 100 |
| Open for another compartment, then assigned-door close | `Opening` | 100 of 100 |
| Assigned door opens for another request ID | `Recovery required` | 100 of 100 |

No sequence without a matching confirmed open followed by a close reached
`Collected`.

The harness also sent a wrong-site result and a wrong-compartment result for
each of 100 assignments in `Opening`. All 200 assignments kept their state and
claim. For another 100 assignments, it reported that the assigned compartment
opened under another request ID. All 100 kept their claim, moved to `Recovery
required`, and never reported the recipient pickup as collecting or collected.

## Expiry boundary

For 2,000 assignments, the harness held the pickup-window end at instant `T` and
released competing valid submissions around that instant.

| Atomic grant instant | Claims granted | Final normal state |
| --- | --- | --- |
| `T - 1 millisecond` | 1,000 of 1,000 | `Opening` |
| `T` | 0 of 500 | `Expired` |
| `T + 1 millisecond` | 0 of 500 | `Expired` |

A claim granted at `T - 1 millisecond` remained in `Opening` after `T`; the
expiry worker did not overwrite it.

## Result

PASS for `CAP-PICKUP.collected-after-open-close`,
`CAP-PICKUP.close-completes-pickup.missing-close`,
`CAP-PICKUP.expire-unclaimed-assignment.window-end`,
`CAP-PICKUP.claim-expiry-race.overlap`, and
`CAP-PICKUP.reject-unmatched-controller-result.wrong-request`.

## Limits

- The run used simulated controller events.
- The controlled product clock had no drift. Production clock accuracy remains
  an external operating assumption.
