# Fictional run 1855: staged release and rollback

This file illustrates a release rehearsal. No executable harness ships with the
OpenIntent repository.

| Field | Value |
| --- | --- |
| Implementation target | `IMPL-PICKUP-SERVICE` |
| Intent revision | `intent-example-17` |
| Build | `example-build-17` with legacy build 4.8 readers |
| Harness | Parcel harness 2.3 |
| Started | 2026-07-11T16:20:00Z |
| Requirement tags | `CAP-PICKUP.one-active-claim`, `CAP-PICKUP.unknown-result-blocks-claim`, `CAP-PICKUP.collected-after-open-close`, `CAP-PICKUP.one-request-id` |

## Procedure

The harness loaded 10,000 old-format assignments, deployed new readers, added
new fields, then started one new worker beside one legacy reader. Legacy writers
remained disabled after the state gate opened. The harness converted 250
in-flight legacy timeout markers to `Recovery required`.

It then simulated the stop trigger, blocked new claims, reconciled every
nonterminal open request, and restored the legacy service only for assignments
that used the old state set.

## Results

| Measure | Expected | Observed |
| --- | --- | --- |
| Old records read by new build | 10,000 | 10,000 |
| New records exposed to a legacy writer | 0 | 0 |
| Legacy timeout markers moved to recovery | 250 | 250 |
| In-flight assignments released without definitive result | 0 | 0 |
| Duplicate logical open requests | 0 | 0 |
| Nonterminal assignments left before rollback | 0 | 0 |
| Missing state-change audit events | 0 | 0 |

## Result

PASS for the rollout and rollback plan. The run supports preservation of
`CAP-PICKUP.one-active-claim`, `CAP-PICKUP.unknown-result-blocks-claim`,
`CAP-PICKUP.collected-after-open-close`, and `CAP-PICKUP.one-request-id`
during the fictional staged release.

## Limits

- The rehearsal did not include a real database engine version upgrade.
- Legacy readers ran, but legacy writers stayed disabled after new states became
  writable.
- Operator staffing and communication were checklist simulations.
