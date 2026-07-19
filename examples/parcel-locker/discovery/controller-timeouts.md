# Discovery: controller timeouts

This file stages fictional evidence from the legacy pickup service. It does not
define product intent.

| Field | Value |
| --- | --- |
| Area | Claim state after an open request timeout |
| Implementation target | `IMPL-PICKUP-SERVICE-LEGACY` |
| Revision | `build-4.8` |
| Environment | Site simulator 2.1 |
| Discoverer | Migration analysis agent, reviewed by Priya Chen |
| Date | 2026-06-26 |
| Related change | `CHG-20260701-CONTROLLER-UNCERTAINTY` |

## Questions being investigated

- Can the product release a claim after the controller response times out?
- Does the controller deduplicate attempts with the same request ID?
- Which actor can resolve an unknown result?

## Source inventory

| Source | Revision or date | What it can show | Limits |
| --- | --- | --- | --- |
| `legacy/controller_client` | build 4.8 | Client retry count, request IDs, and local timeout branch | Cannot show whether hardware executed after a lost response |
| `legacy/pickup_state_test` | build 4.8 | Expected state in the old automated test | Test author and product authority are unknown |
| Incident `INC-204` | 2026-06-14 | One door opened after the service recorded timeout | Site clock differed by up to four seconds |
| Controller contract `LC-7` | revision 7 | Duplicate-request retention and result classes | Does not define behavior after controller reboot |
| Locker Safety Owner interview | 2026-06-27 | Accepted safety priority | Product rules still needed canonical text |

## Claims

| Claim | State | Evidence | Confidence and limits | Next step |
| --- | --- | --- | --- | --- |
| Legacy build 4.8 returns an assignment to `Available` after two timeouts | `OBSERVED` | `legacy/controller_client`; old state test | High for build 4.8 only | Ask whether this is intended or accidental |
| Legacy build 4.8 creates a new open request ID for each controller attempt | `OBSERVED` | `legacy/controller_client` | High for build 4.8 only | Ask whether retries represent one hardware action |
| A timeout can follow a physical open | `OBSERVED` | Incident `INC-204` | Medium; one incident with clock skew | Reproduce with a lost-success response |
| A pickup assignment must not accept a second claim while a prior door open may still execute | `INTENDED` | Locker Safety Owner accepted `CAP-PICKUP.unknown-result-blocks-claim`; pending change at discovery time | Bounded to shared-locker pickup | Add canonical invariant and race evidence |
| The controller retains a result for repeated IDs for 24 hours | `OBSERVED` | Controller contract `LC-7` | High until controller reboot behavior matters | Add as an assumption and test duplicate IDs |
| The controller can prove non-execution after a reboot | `UNKNOWN` | Contract and incident search contain no answer | Material to automatic recovery | Keep reboot result in operator recovery |
| Old code releases the claim, while the safety owner requires the claim held | `CONFLICT` | Legacy build 4.8; safety interview | Direct source conflict | Product owner must choose intended behavior |

## State observed

| From | Event | To | Evidence |
| --- | --- | --- | --- |
| `Opening` | Second timeout | `Available` | Legacy build 4.8 client and state test |
| `Opening` | Late retained success before second timeout | `Collecting` | Controller contract fixture |

## Product decisions needed

| Question with alternatives | Consequence | Product owner | Needed by |
| --- | --- | --- | --- |
| Hold the claim, release it, or mark pickup complete after an unknown result? | Holding needs operator recovery; release can overlap a physical open; complete lacks proof | Parcel Operations Product Owner and Locker Safety Owner | Before intent acceptance |
| Retry twice as legacy code does or set a new bounded policy? | Changes wait time and controller load | Parcel Operations Product Owner | Before `CAP-PICKUP.retry-unknown-result` acceptance |

## Promotion record

| Discovery claim | Intent ID | Change | Accepted by and date |
| --- | --- | --- | --- |
| A possible door open blocks a second claim | `CAP-PICKUP.unknown-result-blocks-claim` | `CHG-20260701-CONTROLLER-UNCERTAINTY` | Jordan Ellis and Sam Okafor, 2026-07-03 |
| Repeated controller attempts use one request ID | `CAP-PICKUP.one-request-id`, `CAP-PICKUP.retry-unknown-result` | `CHG-20260701-CONTROLLER-UNCERTAINTY` | Jordan Ellis, 2026-07-03 |
| Unknown results need operator recovery | `CAP-PICKUP.exhaustion-requires-recovery`, `CAP-PICKUP.reconcile-unknown-result` | `CHG-20260701-CONTROLLER-UNCERTAINTY` | Jordan Ellis and Sam Okafor, 2026-07-03 |
