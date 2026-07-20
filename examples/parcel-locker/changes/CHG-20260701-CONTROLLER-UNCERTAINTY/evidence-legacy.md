# Evidence for CHG-20260701-CONTROLLER-UNCERTAINTY and IMPL-PICKUP-SERVICE-LEGACY

This fictional record checks the legacy target separately. It does not certify
code in this repository.

| Field | Value |
| --- | --- |
| Change | `CHG-20260701-CONTROLLER-UNCERTAINTY` |
| Implementation target | `IMPL-PICKUP-SERVICE-LEGACY` |
| Target kind | Component |
| Intent revision | `intent-example-17` |
| Implementation revision | `build-4.8` |
| Applicable operating profile | `PROF-PEAK-SITE` at `intent-example-17`; not run |
| Applicable normative supporting artifact | None; this target excludes controller contract revision 7 |
| Reviewer | Marcus Bell |
| Review date | 2026-07-12 |
| Environment | Fictional legacy client inspection and site simulator 2.1 |
| Conclusion | Does not conform |

## Scope

- Claim scope: every accepted rule that `intent/index.md` applies to
  `IMPL-PICKUP-SERVICE-LEGACY`
- Affected intent: every product, pickup, and audit rule for this target
- Preserved intent checked for regression: not applicable to this baseline
  review
- Excluded checks and reason: no legacy conformance suite exists, so the map
  keeps every untested rule visible as `NOT RUN`
- Excluded target and reason: `IMPL-PICKUP-SITE-R7` is a separate composition
  and cannot use this component record

## Evidence map

| Intent ID | Check | Conditions | Result | Evidence link | Limits |
| --- | --- | --- | --- | --- | --- |
| `CAP-PICKUP.unknown-result-blocks-claim` | Inspect the final-timeout branch and reproduce two timeouts | Legacy build 4.8 and site simulator 2.1 | FAIL | [Discovery record](../../discovery/controller-timeouts.md) | Shows the named build only |
| `CAP-PICKUP.one-request-id` | Inspect request-ID creation across retries | Legacy build 4.8 | FAIL | [Discovery record](../../discovery/controller-timeouts.md) | Static and fixture evidence do not exercise production hardware |
| `PROD-PARCEL-PICKUP.secret-boundary`, `PROD-PARCEL-PICKUP.actor-scope`, `PROD-PARCEL-PICKUP.audit-read-only` | No current legacy check | Legacy build 4.8 | NOT RUN | none | No result exists for these rules |
| `CAP-PICKUP.one-active-claim`, `CAP-PICKUP.collected-after-open-close`, `CAP-PICKUP.first-valid-claim-wins`, `CAP-PICKUP.first-valid-claim-wins.concurrent-submissions`, `CAP-PICKUP.expire-unclaimed-assignment`, `CAP-PICKUP.expire-unclaimed-assignment.window-end`, `CAP-PICKUP.unavailable-token-disclosure`, `CAP-PICKUP.unavailable-token-disclosure.expired-and-unknown`, `CAP-PICKUP.repeat-token-status`, `CAP-PICKUP.repeat-token-status.lost-claim-response`, `CAP-PICKUP.start-open-request`, `CAP-PICKUP.start-open-request.claim-to-first-attempt`, `CAP-PICKUP.apply-definite-open-result`, `CAP-PICKUP.apply-definite-open-result.executed-and-not-executed`, `CAP-PICKUP.reject-unmatched-controller-result`, `CAP-PICKUP.reject-unmatched-controller-result.wrong-request`, `CAP-PICKUP.retry-unknown-result`, `CAP-PICKUP.retry-unknown-result.lost-success`, `CAP-PICKUP.exhaustion-requires-recovery`, `CAP-PICKUP.exhaustion-requires-recovery.controller-unreachable`, `CAP-PICKUP.reconcile-unknown-result`, `CAP-PICKUP.reconcile-unknown-result.late-success`, `CAP-PICKUP.reconcile-unknown-result.safe-release`, `CAP-PICKUP.restrict-operator-recovery`, `CAP-PICKUP.restrict-operator-recovery.out-of-scope-operator`, `CAP-PICKUP.close-completes-pickup`, `CAP-PICKUP.close-completes-pickup.missing-close`, `CAP-PICKUP.claim-expiry-race`, `CAP-PICKUP.claim-expiry-race.overlap`, `CAP-PICKUP.audit-pickup-actions`, `CAP-PICKUP.audit-pickup-actions.recovery` | No current legacy check | Legacy build 4.8 | NOT RUN | none | No result exists for these rules |
| `QLT-AUDIT.required-event-content`, `QLT-AUDIT.required-event-content.recipient-claim`, `QLT-AUDIT.event-availability`, `QLT-AUDIT.event-availability.peak-site`, `QLT-AUDIT.regional-retention`, `QLT-AUDIT.regional-retention.regional-boundary` | No current legacy check | Legacy build 4.8 | NOT RUN | none | No result exists for these rules |

## Commands and results

The discovery record contains the fictional source inspection and simulator
procedure. This review ran no broader legacy suite.

## SHOULD departures

None. The accepted target scope contains no SHOULD or SHOULD NOT rule.

## Failed, missing, stale, or inconclusive evidence

| Intent ID | Gap | Consequence | Owner | Follow-up |
| --- | --- | --- | --- | --- |
| `CAP-PICKUP.unknown-result-blocks-claim` | Build 4.8 releases a claim after the final timeout | Another claim can overlap a possible door open | Legacy Pickup Service team | Keep the known gap in the intent index until the site joins the 5.x target or another change fixes it |
| `CAP-PICKUP.one-request-id` | Build 4.8 creates a new request ID for each retry | The controller cannot reliably return the first action's retained result | Legacy Pickup Service team | Keep the known gap in the intent index until the site joins the 5.x target or another change fixes it |
| All other applicable IDs listed as `NOT RUN` | No current legacy checks | Reviewers cannot state whether build 4.8 meets those rules | Legacy Pickup Service team | Add evidence if the project continues this release line |

## Freshness review

- Applicable intent or normative terms changed: no
- Implementation moved from `build-4.8`: no
- Applicable operating profile changed: no
- Applicable normative supporting artifact changed: no
- Dependencies, configuration, data, or conditions changed: no known change
- Composition participants changed: not applicable to this component target
- Incidents or observations contradict this result: no

## Reviewer probes

- Negative and unauthorized paths checked: not run
- Failure and recovery paths checked: final controller timeout only
- Concurrent or repeated actions checked: request IDs across retries only
- Data and privacy effects checked: not run
- Quality conditions reproduced: not run

## Conclusion

`Does not conform`

Two applicable absolute rules have `FAIL` results. The many `NOT RUN` rows mean
this record makes no claim about the remaining rules, but those missing results
cannot undo the two demonstrated failures.

Reviewed by Marcus Bell on 2026-07-12.
