# Peak parcel site audit load

| Field | Value |
| --- | --- |
| ID | `PROF-PEAK-SITE` |
| Status | Accepted |
| Product | `PROD-PARCEL-PICKUP` |
| Product authority scope | Pickup data security and audit |
| Accepted change | `CHG-20260701-CONTROLLER-UNCERTAINTY` |
| Applies to targets | `IMPL-PICKUP-SERVICE`, `IMPL-PICKUP-SERVICE-LEGACY`, `IMPL-PICKUP-SITE-R7` |
| Last reviewed | 2026-07-20 |

## Purpose

Auditors need reviewers to reproduce the heaviest supported pickup-event load
because light-load checks cannot establish the audit-search time required by
`QLT-AUDIT.event-availability`.

## Conditions

| Dimension | Required value or range | How a reviewer identifies it |
| --- | --- | --- |
| Workload rate | 500 accepted state-changing pickup actions each second | Product acceptance counter for each one-second interval |
| Workload duration | At least 15 continuous minutes | Timestamped first and final accepted actions |
| Assignment distribution | No assignment supplies more than 5 percent of accepted actions | Per-assignment action counts |
| Service topology | Two service processes with four workers each | Harness process and worker record |
| Audit dependency | Regional audit interface contract revision 1 | Harness dependency record or composition manifest |
| Starting state | Audit search is available and has no earlier unindexed fixture events | A successful pre-run query and a zero-backlog counter |

## Allowed tolerances and exclusions

- The action rate may exceed 500 each second, but it must not fall below 500 in
  a measured interval.
- The run may continue beyond 15 minutes. Reviewers measure at least one
  continuous 15-minute window.
- This profile excludes a deliberately impaired regional network. A different
  profile must govern that condition before evidence can claim support for it.

## Related contracts

- Governing rules: `QLT-AUDIT.event-availability` and
  `QLT-AUDIT.event-availability.peak-site`
- Base or adjacent profiles: None
- External contracts: Regional audit interface contract revision 1

## Review notes

This profile defines test conditions. The latency and completeness thresholds
remain in `QLT-AUDIT.event-availability`. Evidence must record the actual
conditions and every deviation.
