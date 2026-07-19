# Fictional run 1842: concurrent claims

This file illustrates a test report. No executable harness ships with the
OpenIntent repository.

| Field | Value |
| --- | --- |
| Implementation target | `IMPL-PICKUP-SERVICE` |
| Intent revision | `intent-example-17` |
| Build | `example-build-17` |
| Harness | Parcel harness 2.3 |
| Started | 2026-07-10T14:02:11Z |
| Workers | Two service processes, four workers each |
| Assignments | 1,000 independent available assignments |
| Requirement tags | `CAP-PICKUP.one-active-claim`, `CAP-PICKUP.first-valid-claim-wins.concurrent-submissions`, `CAP-PICKUP.repeat-token-status.lost-claim-response` |

## Procedure

For each assignment, the harness released eight valid submissions at one
barrier. It dropped the response to one winning submission, submitted the same
token again, then inspected assignment state, claims, logical open requests, and
controller work.

```text
parcel-harness run pickup.concurrent-claim --build example-build-17 \
  --assignments 1000 --workers 8 --drop-winning-response
```

## Results

| Measure | Expected | Observed |
| --- | --- | --- |
| Assignments with exactly one claim | 1,000 | 1,000 |
| Assignments with more than one claim | 0 | 0 |
| Assignments in `Opening` after the race | 1,000 | 1,000 |
| Logical open requests | 1,000 | 1,000 |
| Pending first-attempt records | 1,000 | 1,000 |
| Repeated tokens that returned current `Opening` state | 1,000 | 1,000 |
| Repeated tokens that created another claim or open request | 0 | 0 |

The harness also terminated a worker after 100 committed claim grants but before
the worker acknowledged its queue read. A replacement worker found all 100
pending controller-work records and did not create a second logical request.

## Result

PASS for `CAP-PICKUP.one-active-claim`,
`CAP-PICKUP.first-valid-claim-wins.concurrent-submissions`, and
`CAP-PICKUP.repeat-token-status.lost-claim-response`.

## Limits

- The run did not terminate the database process during its own commit protocol.
- All workers used one database region with stable latency.
- The harness used the same token for overlapping submissions; it did not model
  physical contention between recipients at the locker.
