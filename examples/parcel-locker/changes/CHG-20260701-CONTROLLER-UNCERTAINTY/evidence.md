# Evidence for CHG-20260701-CONTROLLER-UNCERTAINTY and IMPL-PICKUP-SERVICE

This is a completed fictional record. It demonstrates OpenIntent evidence form
and does not certify code in this repository.

| Field | Value |
| --- | --- |
| Change | `CHG-20260701-CONTROLLER-UNCERTAINTY` |
| Implementation target | `IMPL-PICKUP-SERVICE` |
| Target kind | Component |
| Intent revision | `intent-example-17` |
| Implementation revision | `example-build-17` |
| Operating profiles | `PROF-PEAK-SITE` at `intent-example-17` |
| Normative supporting artifacts | `REF-CONTROLLER-OPEN-V7` at `intent-example-17` |
| Reviewer | Marcus Bell |
| Review date | 2026-07-12 |
| Environment | Fictional parcel harness 2.3, controller simulator 3.2 contract revision 7, two service processes with four workers each, regional audit simulator 1.8 implementing contract revision 1 |
| Conclusion | Conforms |

## Scope

- Claim scope: every accepted rule that `intent/index.md` applies to
  `IMPL-PICKUP-SERVICE`
- Affected intent: the Add and Change rows in `change.md`, including every
  normative scenario under those IDs
- Preserved intent checked for regression: every ID in the Preserve row in
  `change.md`, `PROD-PARCEL-PICKUP.audit-read-only`, and their normative
  scenarios
- Excluded checks and reason: real hardware behavior after a controller reboot
  lies outside the fictional simulator; the accepted rule keeps any result that
  cannot prove execution or non-execution in `Recovery required`
- Excluded target and reason: `IMPL-PICKUP-SITE-R7` is a composition target.
  This component record does not check the assembled physical controller,
  service, and regional audit interface.

## Evidence map

| Intent ID | Check | Conditions | Result | Evidence link | Limits |
| --- | --- | --- | --- | --- | --- |
| `CAP-PICKUP.one-active-claim`, `CAP-PICKUP.first-valid-claim-wins`, `CAP-PICKUP.first-valid-claim-wins.concurrent-submissions`, `CAP-PICKUP.repeat-token-status`, `CAP-PICKUP.repeat-token-status.lost-claim-response` | Race claims and repeat after a lost response | Eight workers, 1,000 assignments | PASS | [run 1842](evidence/run-1842-concurrent-claims.md) | No process loss during the store commit itself |
| `CAP-PICKUP.unknown-result-blocks-claim`, `CAP-PICKUP.exhaustion-requires-recovery`, `CAP-PICKUP.exhaustion-requires-recovery.controller-unreachable` | Lose all controller results, then attempt a new claim | Three timeouts per assignment, 500 assignments | PASS | [run 1848](evidence/run-1848-controller-timeouts.md) | Simulator cannot model unknown firmware defects |
| `PROD-PARCEL-PICKUP.secret-boundary`, `CAP-PICKUP.one-request-id`, `CAP-PICKUP.start-open-request`, `CAP-PICKUP.start-open-request.claim-to-first-attempt`, `CAP-PICKUP.retry-unknown-result`, `CAP-PICKUP.retry-unknown-result.lost-success` | Trace attempt times and request IDs, including a lost success; compare parsed request bodies with `REF-CONTROLLER-OPEN-V7` and inspect forbidden fields and fixture values | Controller simulator revision 7; field order and whitespace may vary | PASS | [run 1848](evidence/run-1848-controller-timeouts.md) | Does not prove behavior on older controllers or a physical controller |
| `CAP-PICKUP.apply-definite-open-result`, `CAP-PICKUP.apply-definite-open-result.executed-and-not-executed`, `CAP-PICKUP.reconcile-unknown-result`, `CAP-PICKUP.reconcile-unknown-result.late-success`, `CAP-PICKUP.reconcile-unknown-result.safe-release` | Apply matching executed, not-executed, unknown, and late results | In-window and expired assignments | PASS | [run 1848](evidence/run-1848-controller-timeouts.md) | A reboot `not found` result deliberately remains unknown |
| `CAP-PICKUP.reject-unmatched-controller-result`, `CAP-PICKUP.reject-unmatched-controller-result.wrong-request` | Send wrong-site, wrong-compartment, and wrong-request results | Matching and mismatching controller fixtures | PASS | [run 1854](evidence/run-1854-state-boundaries.md) | Uses simulated authenticated controllers |
| `PROD-PARCEL-PICKUP.actor-scope`, `PROD-PARCEL-PICKUP.audit-read-only`, `CAP-PICKUP.restrict-operator-recovery`, `CAP-PICKUP.restrict-operator-recovery.out-of-scope-operator` | Try in-scope, out-of-scope, operator, and auditor actions | Two sites and two regions | PASS | [run 1851](evidence/run-1851-permissions-and-audit.md) | Identity service itself is simulated |
| `PROD-PARCEL-PICKUP.secret-boundary`, `CAP-PICKUP.unavailable-token-disclosure`, `CAP-PICKUP.unavailable-token-disclosure.expired-and-unknown`, `CAP-PICKUP.audit-pickup-actions`, `CAP-PICKUP.audit-pickup-actions.recovery`, `QLT-AUDIT.required-event-content`, `QLT-AUDIT.required-event-content.recipient-claim` | Compare unavailable responses and scan event fields for secrets | All unavailable token classes and event types | PASS | [run 1851](evidence/run-1851-permissions-and-audit.md) | Manual field review covers declared schemas, not arbitrary debug logs |
| `QLT-AUDIT.event-availability`, `QLT-AUDIT.event-availability.peak-site` | Run `PROF-PEAK-SITE` for 15 minutes | 500 actions per second; two processes with four workers each; no profile deviation | PASS | [run 1851](evidence/run-1851-permissions-and-audit.md) | Simulated regional store has stable network latency; the profile excludes deliberately impaired networks |
| `QLT-AUDIT.regional-retention`, `QLT-AUDIT.regional-retention.regional-boundary` | Check region isolation and clock-advanced retention | Two regions; 179- and 181-day fixture times | PASS | [run 1851](evidence/run-1851-permissions-and-audit.md) | Clock advance does not prove 180 days of live storage operation |
| `CAP-PICKUP.collected-after-open-close`, `CAP-PICKUP.close-completes-pickup`, `CAP-PICKUP.close-completes-pickup.missing-close` | Permute door events and omit close | 400 pickup sessions | PASS | [run 1854](evidence/run-1854-state-boundaries.md) | Uses controller simulator door events |
| `CAP-PICKUP.expire-unclaimed-assignment`, `CAP-PICKUP.expire-unclaimed-assignment.window-end`, `CAP-PICKUP.claim-expiry-race`, `CAP-PICKUP.claim-expiry-race.overlap` | Grant claims around the exclusive end instant and observe unclaimed expiry | Controlled product clock at `T - 1 ms`, `T`, and `T + 1 ms` | PASS | [run 1854](evidence/run-1854-state-boundaries.md) | Does not measure production clock skew |

## Commands and results

These commands ran in the fictional project harness:

```text
parcel-harness run pickup --change CHG-20260701-CONTROLLER-UNCERTAINTY --target IMPL-PICKUP-SERVICE --runs 1842,1848,1854
parcel-harness run permissions --change CHG-20260701-CONTROLLER-UNCERTAINTY --target IMPL-PICKUP-SERVICE --run 1851
parcel-harness measure audit --profile peak-site --target IMPL-PICKUP-SERVICE --run 1851
parcel-harness run rollout --scenario mixed-workers --target IMPL-PICKUP-SERVICE --run 1855
```

All four commands returned status 0. The linked run records contain counts,
timings, and limits. Run 1855 found no state downgrade or duplicate work across
the fictional mixed-worker rollout.

## SHOULD departures

None. The affected contract contains no unfulfilled SHOULD or SHOULD NOT rule.

## Failed, missing, stale, or inconclusive evidence

None for the named target and revisions. The limits in the evidence map narrow
what the fictional checks establish but do not omit an acceptance condition.

## Freshness review

- Applicable intent or normative terms changed: no
- Implementation moved from `example-build-17`: no
- Applicable operating profile changed: no
- Applicable normative supporting artifact changed: no
- Dependencies, configuration, data, or conditions changed: no
- Composition participants changed: not applicable to this component target
- Incidents or observations contradict this result: no

## Reviewer probes

- Negative and unauthorized paths checked: unknown, malformed, early, expired,
  collected, wrong-site, wrong-region, auditor mutation, and mismatched
  controller inputs
- Failure and recovery paths checked: lost success, three timeouts, definite
  refusal, late success, unknown reconciliation, conflicting request, and
  missing close
- Concurrent or repeated actions checked: eight workers racing, token resubmit,
  duplicate controller attempt, and claim at expiry
- Data and privacy effects checked: declared response and audit schemas scanned
  for raw token, recipient, parcel, controller credential, and cross-site fields
- Quality conditions reproduced: peak-site profile completed for 15 minutes;
  retention used a controlled clock

## Conclusion

`Conforms`

Every affected or preserved invariant, requirement, and normative scenario has
passing fictional-harness evidence for `IMPL-PICKUP-SERVICE` at
`example-build-17` against `intent-example-17`. The stated simulator and
clock-advance limits narrow this conclusion to the named component and
conditions. They do not establish conformance for `IMPL-PICKUP-SITE-R7`.

Reviewed by Marcus Bell on 2026-07-12.
