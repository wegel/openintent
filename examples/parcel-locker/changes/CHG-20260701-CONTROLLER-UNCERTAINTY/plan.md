# Implementation plan for CHG-20260701-CONTROLLER-UNCERTAINTY

This file guides the fictional reference implementation. It does not define
product intent. The accepted files linked from the change record control every
observable choice.

| Field | Value |
| --- | --- |
| Change | `CHG-20260701-CONTROLLER-UNCERTAINTY` |
| Implementation target | `IMPL-PICKUP-SERVICE` |
| Plan owner | Amina Patel |
| Revision | 2026-07-11 |
| Status | Complete for `example-build-17` |

## Intent and scenario coverage

| Intent IDs and normative scenarios | Implementation area | Planned checks | Dependencies |
| --- | --- | --- | --- |
| `CAP-PICKUP.one-active-claim`, `CAP-PICKUP.first-valid-claim-wins`, `CAP-PICKUP.first-valid-claim-wins.concurrent-submissions`, `CAP-PICKUP.repeat-token-status`, `CAP-PICKUP.repeat-token-status.lost-claim-response` | Assignment row and claim handler | Multi-worker claim race and lost client response | Existing assignment store |
| `CAP-PICKUP.unknown-result-blocks-claim`, `CAP-PICKUP.one-request-id`, `CAP-PICKUP.start-open-request`, `CAP-PICKUP.start-open-request.claim-to-first-attempt`, `CAP-PICKUP.apply-definite-open-result`, `CAP-PICKUP.apply-definite-open-result.executed-and-not-executed`, `CAP-PICKUP.reject-unmatched-controller-result`, `CAP-PICKUP.reject-unmatched-controller-result.wrong-request`, `CAP-PICKUP.retry-unknown-result`, `CAP-PICKUP.retry-unknown-result.lost-success`, `CAP-PICKUP.exhaustion-requires-recovery`, `CAP-PICKUP.exhaustion-requires-recovery.controller-unreachable`, `CAP-PICKUP.reconcile-unknown-result`, `CAP-PICKUP.reconcile-unknown-result.late-success`, `CAP-PICKUP.reconcile-unknown-result.safe-release` | Open-request worker and controller client | Timeout, lost success, definite result, mismatched result, late result, and safe release runs | Controller contract revision 7 |
| `CAP-PICKUP.expire-unclaimed-assignment`, `CAP-PICKUP.expire-unclaimed-assignment.window-end`, `CAP-PICKUP.collected-after-open-close`, `CAP-PICKUP.close-completes-pickup`, `CAP-PICKUP.close-completes-pickup.missing-close`, `CAP-PICKUP.claim-expiry-race`, `CAP-PICKUP.claim-expiry-race.overlap` | Door-event handler and product clock | Event permutations and expiry boundary | Site controller clock feed |
| `CAP-PICKUP.unavailable-token-disclosure`, `CAP-PICKUP.unavailable-token-disclosure.expired-and-unknown`, `CAP-PICKUP.restrict-operator-recovery`, `CAP-PICKUP.restrict-operator-recovery.out-of-scope-operator`, `PROD-PARCEL-PICKUP.actor-scope`, `PROD-PARCEL-PICKUP.audit-read-only`, `PROD-PARCEL-PICKUP.secret-boundary` | Recovery endpoint and permission layer | In-scope, out-of-scope, read-only auditor, unavailable-response, and payload inspection | Identity scope claims |
| `CAP-PICKUP.audit-pickup-actions`, `CAP-PICKUP.audit-pickup-actions.recovery`, `QLT-AUDIT.required-event-content`, `QLT-AUDIT.required-event-content.recipient-claim`, `QLT-AUDIT.event-availability`, `QLT-AUDIT.event-availability.peak-site`, `QLT-AUDIT.regional-retention`, `QLT-AUDIT.regional-retention.regional-boundary` | Audit event writer and search projection | Coverage, redaction, throughput, region, and retention runs | Regional audit store |

## Technical approach

The reference implementation stores assignment state, claim ID, logical open
request ID, and a row version in one relational record. A compare-and-swap update
from `Available` to `Opening` chooses the winning claim. The same database
transaction writes a pending controller-work record.

A worker reads pending controller work from a durable queue. It sends the stored
open request ID on each attempt and writes a controller result through a
version-checked state transition. The worker schedules attempt times from the
first-attempt instant and never calculates a new logical request ID.

The recovery endpoint authorizes the operator's site before loading assignment
details. It queries the controller's retained result by the stored request ID and
applies one transition table shared with the late-result handler.

The state transaction also writes a redacted audit outbox event. A separate
projector makes that event searchable. A backlog alert protects the 60-second
absolute audit bound.

These choices are not product requirements. Another implementation may use a
single writer, event log, lock service, or different event transport.

## Technical decisions

| Decision | Reason | Consequence | Revisit when |
| --- | --- | --- | --- |
| Compare-and-swap the assignment row | Existing store supports atomic version checks and makes one winner inspectable | Hot assignments may retry a store write | Claim contention causes measurable store load |
| Persist controller work in the state transaction | A process crash after claim grant cannot lose the first open action | Transaction includes an extra write | Store and worker move to one durable event log |
| Share one result reducer between worker and recovery endpoint | Late and operator-fetched results need identical product transitions | Reducer must remain isolated from transport errors | Another controller adds incompatible result classes |
| Write audit through a transactional outbox | State and its audit event cannot diverge after a process crash | Audit search is eventually consistent | The store supplies an atomic audit interface |

## Data and interface changes

- Add `claim_id`, `open_request_id`, `first_attempt_at`, `attempt_count`, and
  `state_version` to the assignment record.
- Add `Recovery required` to the product-state representation.
- Add controller result lookup by open request ID to the internal controller
  client.
- Keep the external token-submission shape unchanged. Add recipient-safe status
  values already accepted in `CAP-PICKUP`.
- Convert every legacy in-flight timeout marker to `Recovery required` before
  new workers start.

## Work sequence

1. [x] Add read-compatible fields and state representation.
   - Covers: migration support
   - Check: old and new records load in mixed-version harness
   - Depends on: none
2. [x] Make claim grant and controller-work creation atomic.
   - Covers: `CAP-PICKUP.one-active-claim`, `CAP-PICKUP.first-valid-claim-wins`, `CAP-PICKUP.repeat-token-status`, `CAP-PICKUP.start-open-request`
   - Check: run 1842 concurrent claims and crash injection
   - Depends on: task 1
3. [x] Reuse one request ID and apply bounded retry scheduling.
   - Covers: `CAP-PICKUP.unknown-result-blocks-claim`, `CAP-PICKUP.one-request-id`, `CAP-PICKUP.apply-definite-open-result`, `CAP-PICKUP.reject-unmatched-controller-result`, `CAP-PICKUP.retry-unknown-result`, `CAP-PICKUP.exhaustion-requires-recovery`
   - Check: run 1848 controller timeouts
   - Depends on: task 2
4. [x] Add scoped reconciliation with the shared result reducer.
   - Covers: `CAP-PICKUP.reconcile-unknown-result`, `CAP-PICKUP.restrict-operator-recovery`
   - Check: executed, not-executed, unknown, wrong-site, and late-result cases
   - Depends on: task 3
5. [x] Add redacted audit outbox events and regional search checks.
   - Covers: `CAP-PICKUP.audit-pickup-actions`, `QLT-AUDIT.required-event-content`, `QLT-AUDIT.event-availability`, and `QLT-AUDIT.regional-retention`
   - Check: run 1851 audit and permission exercise
   - Depends on: tasks 2 and 4
6. [x] Rehearse state migration, mixed workers, rollout stop, and rollback.
   - Covers: preserved invariants during release
   - Check: run 1855 staged release exercise
   - Depends on: tasks 1 through 5

## Rollout and recovery

| Stage | Entry check | Observable result | Stop or rollback trigger | Recovery action |
| --- | --- | --- | --- | --- |
| Read compatibility | New build reads old and new assignment shapes | No recipient change | Any record cannot load | Stop deploy and keep old writers |
| One internal site | Controller revision 7 and staffed operator confirmed | New recovery result appears only after injected timeout | Invariant failure or audit event over 60 seconds | Stop claims; reconcile nonterminal assignments |
| Ten sites | Recovery demand below 2 percent and no scope denial defect | Normal recipients see no changed path | Demand above staffing bound or wrong-site data appears | Disable new claims at affected sites and investigate |
| Full rollout | Seven days of accepted site results | All revision 7 sites use new behavior | Safety, secret, or state invariant fails | Stop upgraded-site claims and follow per-site reconciliation runbook |

## Discoveries during implementation

| Discovery | Kind | Action | Owner |
| --- | --- | --- | --- |
| A late success may arrive after all normal attempts finish | Product | Revised `CAP-PICKUP.reconcile-unknown-result` and added its late-success scenario; returned intent to review | Product authority reaccepted 2026-07-08 |
| Controller `not found` does not prove non-execution after reboot | Product | Keep `Recovery required`; the revised reconciliation rule requires definite non-execution and a closed door | Product authority confirmed 2026-07-08 |
| A controller may report the assigned compartment under an unrelated request ID | Product | Added `CAP-PICKUP.reject-unmatched-controller-result` and returned the mismatched-result behavior to review | Product authority reaccepted 2026-07-08 |
| Audit projector batches improve peak latency | Technical | Use bounded batches of 200 events | Audit implementation owner |

## Handoff

- Completed: tasks 1 through 6 in `example-build-17`
- Checks run: fictional runs 1842, 1848, 1851, 1854, and 1855
- Open blockers: none
- Next action: independent conformance review of the linked evidence
