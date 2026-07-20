# CHG-20260701-CONTROLLER-UNCERTAINTY: Hold pickup state through unknown opens

| Field | Value |
| --- | --- |
| ID | `CHG-20260701-CONTROLLER-UNCERTAINTY` |
| Change state | Completed |
| Intent checkpoint | Accepted |
| Author | Priya Chen |
| Affected products | `PROD-PARCEL-PICKUP` |
| Cross-product coordinator | Not applicable |
| Product authority scopes | Parcel pickup behavior; locker custody safety; pickup data security and audit |
| Created | 2026-07-01 |
| Target release | Pickup service 5.0 |
| Proposed intent revision | `intent-example-17` |
| Accepted intent revision | `intent-example-17` |
| Overlapping changes | None |

## Why now

Incident `INC-204` showed a compartment door opening after the legacy client had
timed out and returned the assignment to `Available`. A second valid claim could
then overlap a possible physical open. The legacy client also used a new request
ID for each retry, so the controller could not reliably return its retained
result.

The [discovery record](../../discovery/controller-timeouts.md) found that the old
behavior conflicted with the Locker Safety Owner's custody rule.

## Intended outcome

A recipient can continue or recover one pickup after missing controller replies
while the product prevents another claim until it knows the first open did not
execute.

## Non-goals

- **NON-GOAL:** This change does not alter token creation or delivery.
- **NON-GOAL:** This change does not let the service bypass the controller or
  force a physical door action.
- **NON-GOAL:** This change does not infer parcel removal from a door-open event.

## Context packet

An implementer or reviewer should read:

- `intent/index.md`
- `intent/product.md#product-invariants`
- `intent/glossary.md`
- `intent/capabilities/CAP-PICKUP.md`
- `intent/qualities/QLT-AUDIT.md`
- `intent/profiles/PROF-PEAK-SITE.md`
- `intent/references/REF-CONTROLLER-OPEN-V7.md`
- `intent/decisions/DEC-0001.md`
- `discovery/controller-timeouts.md`

## Intent edits

| Kind | Intent IDs | Canonical file | Summary |
| --- | --- | --- | --- |
| Add | `CAP-PICKUP.unknown-result-blocks-claim`, `CAP-PICKUP.one-request-id` | `intent/capabilities/CAP-PICKUP.md` | Block new claims during an unknown open and reuse one request ID |
| Add | `CAP-PICKUP.retry-unknown-result`, `CAP-PICKUP.exhaustion-requires-recovery`, `CAP-PICKUP.reconcile-unknown-result`, `CAP-PICKUP.restrict-operator-recovery` | `intent/capabilities/CAP-PICKUP.md` | Bound retries, enter recovery, reconcile definite results, and scope operators |
| Add | `CAP-PICKUP.expire-unclaimed-assignment`, `CAP-PICKUP.apply-definite-open-result`, `CAP-PICKUP.reject-unmatched-controller-result` | `intent/capabilities/CAP-PICKUP.md` | Make expiry and matching controller-result transitions explicit normative duties |
| Add | `QLT-AUDIT.required-event-content`, `QLT-AUDIT.event-availability`, `QLT-AUDIT.regional-retention` | `intent/qualities/QLT-AUDIT.md` | Make recovery actions timely, scoped, retained, and free of bearer secrets |
| Add | `PROF-PEAK-SITE` | `intent/profiles/PROF-PEAK-SITE.md` | Define the conditions for the accepted peak-site audit check without copying its thresholds |
| Add | `REF-CONTROLLER-OPEN-V7` | `intent/references/REF-CONTROLLER-OPEN-V7.md`, `intent/references/controller-open-v7.json` | Fix the controller revision 7 request fields and meanings in one reviewable fixture |
| Add | `PROD-PARCEL-PICKUP.audit-read-only` | `intent/product.md` | Make an auditor's read-only product boundary explicit |
| Change | `CAP-PICKUP.start-open-request` | `intent/capabilities/CAP-PICKUP.md` | Define one logical open request, its revision 7 body, and a two-second first-attempt bound |
| Change | `CAP-PICKUP.audit-pickup-actions` | `intent/capabilities/CAP-PICKUP.md` | Cover controller and operator recovery events in audit |
| Preserve | `PROD-PARCEL-PICKUP.secret-boundary`, `PROD-PARCEL-PICKUP.actor-scope`, `CAP-PICKUP.one-active-claim`, `CAP-PICKUP.collected-after-open-close`, `CAP-PICKUP.first-valid-claim-wins`, `CAP-PICKUP.unavailable-token-disclosure`, `CAP-PICKUP.repeat-token-status`, `CAP-PICKUP.close-completes-pickup`, `CAP-PICKUP.claim-expiry-race` | Product and pickup intent | Preserve secret, scope, single-claim, winner, completion, disclosure, repeat, close, and expiry rules |

## Implementation targets

| Target ID | Kind | Owner | Checkpoint | Implementation revision | Components or participants | Current deployed behavior | Latest evidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `IMPL-PICKUP-SERVICE` | Component | Priya Chen, Pickup Service | Conformant | `example-build-17` | None; evidence uses named simulators | Fictional component build checked with a controller revision 7 simulator; this target does not include a physical site | `evidence.md` |
| `IMPL-PICKUP-SERVICE-LEGACY` | Component | Legacy Pickup Service team | Nonconformant | `build-4.8` | None; evidence uses the legacy site simulator | Older-controller sites retain build 4.8 and its two known gaps until they can join the 5.x target | `evidence-legacy.md` |

`IMPL-PICKUP-SITE-R7` was registered after this completed change. It is not an
affected target of this historical record. The current intent index tracks its
separate `Unknown` checkpoint and missing composition evidence.

## Compatibility and migration

- Existing recipients may see operator-help instead of an immediate rescan after
  the controller remains unknown.
- Assignments already in the legacy retry state migrate to `Recovery required`.
  They do not return to `Available` automatically.
- Controller contract revision 7 already accepts repeated request IDs. Older
  controller sites remain on pickup service 4.8 until upgraded.
- The service deploys read support for the new states before workers start
  writing them.
- Rollback stops new claims at upgraded sites and lets site operators reconcile
  every `Opening` or `Recovery required` assignment before service 4.8 resumes.

## Risks

| Risk | Affected actor | Prevention or detection | Recovery owner |
| --- | --- | --- | --- |
| A request ID changes across retries | Recipient and parcel custodian | Controller trace check for `CAP-PICKUP.one-request-id` | Pickup service on-call |
| A harmless timeout sends too many recipients to operators | Recipient and site operator | Recovery-rate monitor by site and controller version | Parcel Operations |
| Operator scope exposes another site's assignment | Recipient | Negative site-scope tests and audit review | Security on-call |
| Partial rollout lets an old worker release a new state | Recipient | Versioned state writer gate and mixed-worker rehearsal | Release owner |
| Audit delay hides recovery actions | Auditor | `QLT-AUDIT.event-availability` peak-site exercise and alert | Audit platform owner |

## Assumptions

- **ASSUMPTION:** Controller revision 7 retains a request result for 24 hours and
  treats a repeated ID as the same physical action.
- **ASSUMPTION:** Each upgraded site has a staffed Site Recovery role during its
  pickup hours.

## Open questions

None. Controller behavior after a reboot remains unknown, but the accepted
product rule keeps the assignment in `Recovery required`; that unknown does not
change conformance.

## Approval record

| Review | Proposed revision or target | Intent IDs | Named approver or reviewer | Date | Result and notes |
| --- | --- | --- | --- | --- | --- |
| Intent review | `intent-example-17` | All Add and Change rows except security-specific rules | Jordan Ellis and Sam Okafor | 2026-07-03 | Accepted; Sam accepted the claim-retention safety choice |
| Security and audit review | `intent-example-17` | `PROD-PARCEL-PICKUP.secret-boundary`, `PROD-PARCEL-PICKUP.audit-read-only`, `CAP-PICKUP.restrict-operator-recovery`, `QLT-AUDIT` and descendants, `PROF-PEAK-SITE` | Elena Ruiz | 2026-07-05 | Accepted |
| Locker contract review | `intent-example-17` | `CAP-PICKUP.start-open-request`, `CAP-PICKUP.one-request-id`, `REF-CONTROLLER-OPEN-V7` | Sam Okafor | 2026-07-05 | Accepted the revision 7 body and its allowed variations |
| Intent re-review | `intent-example-17` | `CAP-PICKUP.apply-definite-open-result`, `CAP-PICKUP.reject-unmatched-controller-result`, `CAP-PICKUP.reconcile-unknown-result` and its scenarios | Jordan Ellis and Sam Okafor | 2026-07-08 | Accepted after implementation probes exposed late and mismatched controller results |
| Evidence review | `IMPL-PICKUP-SERVICE` at `example-build-17` | All affected and preserved IDs | Marcus Bell | 2026-07-12 | Conforms against `intent-example-17` with the limits in `evidence.md` |

## Completion rule

This change is complete when product authority has accepted every listed intent
edit, `IMPL-PICKUP-SERVICE` has current conformance evidence for
`example-build-17` against `intent-example-17`, and the legacy target records
its excluded rollout scope and known result honestly. All conditions are met.

## Next action

No change action remains. Parcel Operations monitors recovery demand as normal
fictional product operation.
