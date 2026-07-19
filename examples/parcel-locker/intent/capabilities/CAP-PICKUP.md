# Collect a parcel

| Field | Value |
| --- | --- |
| ID | `CAP-PICKUP` |
| Status | Accepted |
| Product authority scope | Parcel pickup behavior; locker custody safety; pickup data security and audit |
| Accepted change | `CHG-20260701-CONTROLLER-UNCERTAINTY` |
| Last reviewed | 2026-07-19 |
| Read with | `intent/glossary.md`, `intent/qualities/QLT-AUDIT.md`, `intent/decisions/DEC-0001.md` |

## Outcome and boundary

A recipient can use a valid pickup token to open one assigned compartment and
finish a pickup session. A site operator can resolve an unknown controller
result without permitting a second recipient action to overlap the first.

This capability begins when the fulfillment system registers an assignment in
the `Available` state. It ends when the assignment reaches `Collected` or
`Expired`. The fulfillment system owns token delivery and expired-parcel
removal. The locker controller owns physical lock and door sensing.

### Non-goals

- **NON-GOAL:** The product does not identify the person holding the bearer
  token.
- **NON-GOAL:** The product does not prove that a parcel left the compartment.
- **NON-GOAL:** A site operator cannot bypass the locker controller through this
  capability.

## Actors and permissions

| Actor | Allowed summary | Forbidden summary | Scope | Governing intent IDs |
| --- | --- | --- | --- | --- |
| Recipient | Submit a pickup token and view a recipient-safe result | View assignment metadata before a valid token claim or act on another assignment | Assignment authorized by the bearer token | `PROD-PARCEL-PICKUP.secret-boundary`, `PROD-PARCEL-PICKUP.actor-scope`, `CAP-PICKUP.first-valid-claim-wins`, `CAP-PICKUP.unavailable-token-disclosure`, `CAP-PICKUP.repeat-token-status` |
| Site operator | View state, request controller reconciliation, and release a safely closed assignment | Read the token, mark an assignment collected, or act outside assigned sites | Named locker sites granted to the Site Recovery role | `PROD-PARCEL-PICKUP.secret-boundary`, `PROD-PARCEL-PICKUP.actor-scope`, `CAP-PICKUP.reconcile-unknown-result`, `CAP-PICKUP.restrict-operator-recovery` |
| Auditor | Read state-change audit events | Read raw tokens or mutate an assignment | Named operating regions | `PROD-PARCEL-PICKUP.secret-boundary`, `PROD-PARCEL-PICKUP.actor-scope`, `PROD-PARCEL-PICKUP.audit-read-only`, `QLT-AUDIT.regional-retention` |
| Locker controller | Report results for a logical open request and door events | Change product state without a matching request or compartment | Controller's authenticated site | `CAP-PICKUP.apply-definite-open-result`, `CAP-PICKUP.reject-unmatched-controller-result`, `CAP-PICKUP.collected-after-open-close` |

## Terms

Shared terms appear in [the product glossary](../glossary.md).

- **Pickup window:** A half-open time range from its start instant, inclusive, to
  its end instant, exclusive.
- **Recipient-safe result:** A result that contains no recipient identity, raw
  token, parcel metadata, or assignment metadata beyond the locker site and
  current pickup instruction.

## State model

| State | Meaning | Entry summary | Exit summary | Governing intent IDs |
| --- | --- | --- | --- | --- |
| `Available` | The pickup window permits one valid token claim | Fulfillment registers the assignment; safe recovery releases an unexecuted request | A claim wins or the window ends | `CAP-PICKUP.first-valid-claim-wins`, `CAP-PICKUP.expire-unclaimed-assignment`, `CAP-PICKUP.apply-definite-open-result`, `CAP-PICKUP.reconcile-unknown-result`, `CAP-PICKUP.claim-expiry-race` |
| `Opening` | One claim owns the assignment and the product seeks a definite controller result | First valid claim | Controller confirms execution or non-execution, or attempts exhaust | `CAP-PICKUP.first-valid-claim-wins`, `CAP-PICKUP.start-open-request`, `CAP-PICKUP.apply-definite-open-result`, `CAP-PICKUP.retry-unknown-result`, `CAP-PICKUP.exhaustion-requires-recovery`, `CAP-PICKUP.unknown-result-blocks-claim` |
| `Collecting` | The controller confirmed that the assigned door opened | A matching result confirms the logical request executed | Door closes or the close wait expires | `CAP-PICKUP.apply-definite-open-result`, `CAP-PICKUP.reconcile-unknown-result`, `CAP-PICKUP.close-completes-pickup`, `CAP-PICKUP.collected-after-open-close` |
| `Recovery required` | The product cannot prove a safe normal transition | Open attempts exhaust, a door does not close, or the controller reports a conflicting state | Site operator reconciliation proves the next safe state | `CAP-PICKUP.exhaustion-requires-recovery`, `CAP-PICKUP.reconcile-unknown-result`, `CAP-PICKUP.close-completes-pickup`, `CAP-PICKUP.reject-unmatched-controller-result` |
| `Collected` | The assigned door opened and later closed during this pickup session | The assigned door closes after a confirmed matching open | Terminal | `CAP-PICKUP.collected-after-open-close`, `CAP-PICKUP.close-completes-pickup` |
| `Expired` | The pickup window ended before a claim won, or safe recovery finished after expiry | The window ends in `Available`; a definite non-execution or safe recovery releases after expiry | Terminal for recipient pickup | `CAP-PICKUP.expire-unclaimed-assignment`, `CAP-PICKUP.apply-definite-open-result`, `CAP-PICKUP.reconcile-unknown-result`, `CAP-PICKUP.claim-expiry-race` |

### Legal transitions

| From | Event and conditions | To | Actor-visible result | Governing intent IDs |
| --- | --- | --- | --- | --- |
| `Available` | First valid token submission wins during the pickup window | `Opening` | Recipient sees that the door is opening | `CAP-PICKUP.first-valid-claim-wins`, `CAP-PICKUP.claim-expiry-race` |
| `Available` | Pickup window ends before a claim wins | `Expired` | Later submissions receive the generic unavailable result | `CAP-PICKUP.expire-unclaimed-assignment`, `CAP-PICKUP.unavailable-token-disclosure` |
| `Opening` | A matching controller result confirms that the logical open request executed and the door is open | `Collecting` | Recipient may open the door and remove the parcel | `CAP-PICKUP.apply-definite-open-result` |
| `Opening` | A matching controller result definitively reports that the request did not execute | `Available` or `Expired` | Recipient may retry during the window or contact support after expiry | `CAP-PICKUP.apply-definite-open-result` |
| `Opening` | All allowed attempts end without a definite result | `Recovery required` | Recipient receives the operator-help result | `CAP-PICKUP.exhaustion-requires-recovery` |
| `Collecting` | Controller reports the assigned door closed for the logical request | `Collected` | Recipient sees pickup complete | `CAP-PICKUP.collected-after-open-close`, `CAP-PICKUP.close-completes-pickup` |
| `Collecting` | No close appears within two minutes | `Recovery required` | Recipient sees that operator help is required | `CAP-PICKUP.close-completes-pickup` |
| `Recovery required` | Reconciliation confirms the prior request executed and the door is open | `Collecting` | Operator sees the confirmed open session | `CAP-PICKUP.reconcile-unknown-result` |
| `Recovery required` | Reconciliation proves no open executed and the door is closed | `Available` or `Expired` | Operator sees that recipient pickup may resume or has expired | `CAP-PICKUP.reconcile-unknown-result` |

## Invariants

### CAP-PICKUP.one-active-claim One active claim

The Parcel Pickup Coordinator MUST hold at most one active claim for an
assignment.

### CAP-PICKUP.unknown-result-blocks-claim Unknown results block a new claim

From the first controller attempt until the controller definitively reports that
the logical open request did not execute or the pickup reaches a terminal state,
the Parcel Pickup Coordinator MUST NOT make the assignment available to a new
claim.

### CAP-PICKUP.collected-after-open-close Collected requires an open and close

The Parcel Pickup Coordinator MUST NOT mark an assignment `Collected` unless the
locker controller reported the assigned door open for the claim's logical open
request and later reported that door closed.

### CAP-PICKUP.one-request-id One identity across retries

The Parcel Pickup Coordinator MUST use one open request ID for every controller
attempt that belongs to the same logical open request.

## Requirements

### CAP-PICKUP.first-valid-claim-wins First valid claim wins

When one or more valid token submissions overlap for an `Available` assignment,
the Parcel Pickup Coordinator MUST grant exactly one claim, move the assignment
to `Opening`, and prevent every other submission from creating a claim.

#### CAP-PICKUP.first-valid-claim-wins.concurrent-submissions Concurrent valid submissions

This scenario is normative.

- GIVEN an `Available` assignment and two overlapping submissions of its valid
  token
- WHEN two service workers handle the submissions concurrently
- THEN one submission creates the assignment's only claim
- AND both workers observe the assignment in `Opening` after they finish
- AND only one logical open request exists

### CAP-PICKUP.expire-unclaimed-assignment Expire an unclaimed assignment

When an assignment remains `Available` at the exclusive end of its pickup
window, the Parcel Pickup Coordinator MUST move it to `Expired` and MUST return
the recipient-safe unavailable result for every later token submission.

#### CAP-PICKUP.expire-unclaimed-assignment.window-end Pickup window ends without a claim

This scenario is normative.

- GIVEN an `Available` assignment whose pickup window ends at `T`
- WHEN no claim wins before `T`
- THEN the assignment moves to `Expired` at `T`
- AND a later submission of its former valid token receives the same
  recipient-safe unavailable result as an unknown token

### CAP-PICKUP.unavailable-token-disclosure Invalid and unavailable tokens disclose no assignment

For a malformed, unknown, early, expired, already collected, or otherwise
unavailable token, the Parcel Pickup Coordinator MUST return the same
recipient-safe unavailable result and MUST NOT reveal whether an assignment
exists.

#### CAP-PICKUP.unavailable-token-disclosure.expired-and-unknown Expired and unknown tokens

This scenario is normative.

- GIVEN one token for an expired assignment and one random value
- WHEN a caller submits each value
- THEN both responses have the same status class and recipient-safe body shape
- AND neither response contains an assignment ID, compartment, parcel data, or
  recipient data

### CAP-PICKUP.repeat-token-status A repeated valid token reports current pickup state

After a valid token creates a claim, the Parcel Pickup Coordinator MUST let a
later submission of that token view the current recipient-safe pickup state
without creating another claim or logical open request.

#### CAP-PICKUP.repeat-token-status.lost-claim-response Lost claim response

This scenario is normative.

- GIVEN a valid token created a claim but the recipient did not receive the
  response
- WHEN the recipient submits the token again while the assignment is `Opening`
- THEN the recipient sees that the door is opening
- AND the assignment still has one claim and one logical open request

### CAP-PICKUP.start-open-request Start the open request

After granting a claim, the Parcel Pickup Coordinator MUST create one logical
open request for the assigned site and compartment, then send its first
controller attempt within two seconds.

#### CAP-PICKUP.start-open-request.claim-to-first-attempt Claim to first attempt

This scenario is normative.

- GIVEN a valid claim at time `T`
- WHEN the controller connection is available
- THEN the first attempt carries the assigned site and compartment and one new
  open request ID
- AND the product sends the attempt no later than `T + 2 seconds`

### CAP-PICKUP.apply-definite-open-result Apply a definite open result

For an authenticated controller result whose site, compartment, and open
request ID match an assignment in `Opening`, the Parcel Pickup Coordinator MUST
move the assignment to `Collecting` when the controller confirms execution and
the assigned door is open. When the controller definitively confirms that the
request did not execute, the product MUST end the claim and move the assignment
to `Available` if its pickup window remains open or `Expired` otherwise.

#### CAP-PICKUP.apply-definite-open-result.executed-and-not-executed Matching definite results

This scenario is normative.

- GIVEN two assignments in `Opening`, one inside its pickup window and one after
  its pickup window
- WHEN matching controller results confirm execution with the assigned door
  open for the first and definite non-execution for the second
- THEN the first assignment moves to `Collecting` and keeps its claim
- AND the second assignment moves to `Expired` and ends its claim

### CAP-PICKUP.reject-unmatched-controller-result Reject an unmatched controller result

When a controller result has a site, compartment, or open request ID that does
not match the assignment's logical open request, the Parcel Pickup Coordinator
MUST NOT treat it as proof that the logical request executed or did not execute.
For a result about another site or compartment, the product MUST keep the
assignment's state and claim unchanged. If a result says the assigned
compartment opened for another request ID, the product MUST retain the claim and
move the assignment to `Recovery required`.

#### CAP-PICKUP.reject-unmatched-controller-result.wrong-request Wrong request result

This scenario is normative.

- GIVEN an assignment in `Opening` and an authenticated controller at its site
- WHEN that controller reports that the assigned compartment opened for another
  request ID
- THEN the assignment moves to `Recovery required` with its original claim
- AND the product does not report the pickup as collecting or collected

### CAP-PICKUP.retry-unknown-result Retry an unknown controller result

When a controller attempt times out or returns a result that does not prove
executed or not executed, the Parcel Pickup Coordinator MUST make no more than
three total attempts for the logical open request, MUST reuse its open request ID
for each attempt, and MUST finish those attempts within 20 seconds of the first
attempt unless a definite result arrives sooner.

#### CAP-PICKUP.retry-unknown-result.lost-success Lost success response

This scenario is normative.

- GIVEN the controller opens the door for the first attempt but its response is
  lost
- WHEN the product retries the logical open request
- THEN every retry carries the first attempt's open request ID
- AND the controller may return its retained success result
- AND the product moves the assignment to `Collecting` without issuing another
  logical open request

### CAP-PICKUP.exhaustion-requires-recovery Exhaustion requires operator recovery

When all allowed attempts finish without a definite controller result, the
Parcel Pickup Coordinator MUST move the assignment to `Recovery required`, MUST
retain the claim, and MUST give the recipient an operator-help result within 25
seconds of the first attempt.

#### CAP-PICKUP.exhaustion-requires-recovery.controller-unreachable Controller remains unreachable

This scenario is normative.

- GIVEN an assignment in `Opening`
- WHEN all three controller attempts time out
- THEN the assignment reaches `Recovery required`
- AND the existing claim remains active
- AND the token reports that operator help is required
- AND another token submission cannot create a claim

### CAP-PICKUP.reconcile-unknown-result Reconcile an unknown open result

The Parcel Pickup Coordinator MUST let a site operator with scope for the
assignment's site request reconciliation. It MUST query the controller by the
original open request ID and MUST apply only these results:

- confirmed executed with the door open moves the assignment to `Collecting`;
- confirmed not executed with the door closed releases the claim and moves the
  assignment to `Available` when the pickup window remains open or `Expired`
  otherwise; and
- any other result leaves the assignment in `Recovery required`.

#### CAP-PICKUP.reconcile-unknown-result.late-success Late controller success

This scenario is normative.

- GIVEN an assignment in `Recovery required` after three timeouts
- WHEN reconciliation returns that the original request executed and the door is
  open
- THEN the assignment moves to `Collecting`
- AND the original claim remains the only claim
- AND the product does not issue a new open request

#### CAP-PICKUP.reconcile-unknown-result.safe-release Safe release after non-execution

This scenario is normative.

- GIVEN an assignment in `Recovery required` during its pickup window
- WHEN reconciliation proves that the original request did not execute and the
  assigned door is closed
- THEN the assignment moves to `Available`
- AND the old claim ends
- AND the same valid token may create a new claim

### CAP-PICKUP.restrict-operator-recovery Restrict operator recovery

The Parcel Pickup Coordinator MUST let only a Site Recovery actor assigned to the
locker site request reconciliation, MUST NOT let that actor mark an assignment
`Collected`, and MUST NOT expose the raw pickup token to that actor.

#### CAP-PICKUP.restrict-operator-recovery.out-of-scope-operator Out-of-scope operator

This scenario is normative.

- GIVEN an operator with Site Recovery permission for another site
- WHEN the operator requests reconciliation for this assignment
- THEN the product denies the request
- AND the response does not contain assignment, parcel, recipient, token, or
  controller-result data
- AND the assignment state remains unchanged

### CAP-PICKUP.close-completes-pickup Close completes the pickup session

After the controller confirms the assigned door open, the Parcel Pickup
Coordinator MUST move the assignment to `Collected` on the next confirmed close
for that door. If no close arrives within two minutes of the confirmed open, the
product MUST move the assignment to `Recovery required` instead.

#### CAP-PICKUP.close-completes-pickup.missing-close Missing close event

This scenario is normative.

- GIVEN the assignment is `Collecting` after a confirmed open at time `T`
- WHEN no close event arrives by `T + 2 minutes`
- THEN the assignment moves to `Recovery required`
- AND the product does not mark it `Collected`

### CAP-PICKUP.claim-expiry-race Resolve the expiry race at claim grant

The Parcel Pickup Coordinator MUST evaluate the pickup window at the instant it
grants the claim. A claim granted before the exclusive end instant remains valid
after that instant; a submission that has not won by the end instant MUST NOT
create a claim.

#### CAP-PICKUP.claim-expiry-race.overlap Claim overlaps expiry

This scenario is normative.

- GIVEN an `Available` assignment whose pickup window ends at `T`
- WHEN two valid submissions overlap `T`
- THEN a claim granted before `T` continues in `Opening`
- AND a submission that did not win before `T` cannot create a claim

### CAP-PICKUP.audit-pickup-actions Audit state and recovery actions

The Parcel Pickup Coordinator MUST create the events required by
[`QLT-AUDIT`](../qualities/QLT-AUDIT.md) for each claim grant, controller result,
state transition, and operator reconciliation request.

#### CAP-PICKUP.audit-pickup-actions.recovery Recovery audit

This scenario is normative.

- GIVEN a site operator requests reconciliation
- WHEN the product applies the controller result
- THEN audit events identify the operator, assignment, site, original open
  request ID, prior state, result class, and resulting state
- AND no event contains the raw pickup token

## Assumptions and external dependencies

- **ASSUMPTION:** The controller treats duplicate open request IDs as the same
  logical hardware action for at least 24 hours.
- **ASSUMPTION:** The controller can definitively report `executed` or `not
  executed` for a retained request, or say that it cannot determine the result.
- The product clock supplies instants with no more than one second of error from
  the clock that created the pickup window.

If the controller violates its duplicate-request promise, the product keeps the
assignment in `Recovery required` and alerts a site operator. It does not issue a
new logical open request automatically.

## Unspecified observable behavior

- **UNSPECIFIED:** Implementations may choose retry spacing within the two-second
  first-attempt and 20-second total bounds.
- **UNSPECIFIED:** Implementations may choose the recipient-safe wording and
  presentation while preserving the required information boundary.

## Acceptance map

| Intent ID | Evidence needed |
| --- | --- |
| `CAP-PICKUP.one-active-claim`, `CAP-PICKUP.first-valid-claim-wins`, `CAP-PICKUP.first-valid-claim-wins.concurrent-submissions` | A controlled race with several workers, one assignment, and final claim and open-request counts |
| `CAP-PICKUP.expire-unclaimed-assignment`, `CAP-PICKUP.expire-unclaimed-assignment.window-end` | A controlled-clock run that observes state and response at the exclusive window end |
| `CAP-PICKUP.unknown-result-blocks-claim`, `CAP-PICKUP.exhaustion-requires-recovery`, `CAP-PICKUP.exhaustion-requires-recovery.controller-unreachable` | Fault injection that loses every controller result and tries another claim before recovery |
| `CAP-PICKUP.collected-after-open-close`, `CAP-PICKUP.close-completes-pickup`, `CAP-PICKUP.close-completes-pickup.missing-close` | Event-sequence tests for close-before-open, open-then-close, and missing close |
| `CAP-PICKUP.one-request-id`, `CAP-PICKUP.retry-unknown-result`, `CAP-PICKUP.retry-unknown-result.lost-success` | A controller trace that compares request IDs across timeouts and a lost-success response |
| `CAP-PICKUP.unavailable-token-disclosure`, `CAP-PICKUP.unavailable-token-disclosure.expired-and-unknown` | Paired black-box responses for each unavailable token class and a disclosure review |
| `CAP-PICKUP.repeat-token-status`, `CAP-PICKUP.repeat-token-status.lost-claim-response` | A lost-response test that repeats the valid token and counts claims and open requests |
| `CAP-PICKUP.start-open-request`, `CAP-PICKUP.start-open-request.claim-to-first-attempt` | A timed claim-to-controller trace at the two-second boundary |
| `CAP-PICKUP.apply-definite-open-result`, `CAP-PICKUP.apply-definite-open-result.executed-and-not-executed` | Matching executed and non-executed result checks inside and after the pickup window |
| `CAP-PICKUP.reject-unmatched-controller-result`, `CAP-PICKUP.reject-unmatched-controller-result.wrong-request` | Results with a wrong site, compartment, and request ID while state and claim are inspected |
| `CAP-PICKUP.reconcile-unknown-result`, `CAP-PICKUP.reconcile-unknown-result.late-success`, `CAP-PICKUP.reconcile-unknown-result.safe-release` | Reconciliation tests for executed, not executed, unknown, and late results |
| `CAP-PICKUP.restrict-operator-recovery`, `CAP-PICKUP.restrict-operator-recovery.out-of-scope-operator` | Positive and negative site-scope tests plus token-field inspection |
| `CAP-PICKUP.claim-expiry-race`, `CAP-PICKUP.claim-expiry-race.overlap` | A controlled clock test on both sides of the exclusive expiry instant |
| `CAP-PICKUP.audit-pickup-actions`, `CAP-PICKUP.audit-pickup-actions.recovery` | Audit-event coverage and secret-redaction inspection under `QLT-AUDIT` |

## Examples

- **EXAMPLE:** A controller that opens the door but loses its response returns
  the prior success when it receives the same request ID. The assignment moves
  from `Opening` to `Collecting` without a second physical open action.
- **EXAMPLE:** A controller that cannot find the request does not by itself prove
  non-execution. The assignment remains `Recovery required` until the controller
  also confirms that the door stayed closed under its retained-result contract.
