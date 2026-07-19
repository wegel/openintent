# Intent index

| Field | Value |
| --- | --- |
| Product | Parcel Pickup Coordinator |
| OpenIntent version | `0.1` |
| Accepted branch | `main` |
| Contract state | Accepted |
| Last reviewed | 2026-07-19 |

This file routes readers to the smallest useful context set. It does not
restate requirements.

## Product authority registry

| Scope | Authority | May delegate | Conflict resolver | Acceptance record |
| --- | --- | --- | --- | --- |
| Parcel pickup behavior | Parcel Operations Product Owner, exercised by Jordan Ellis | May delegate named IDs in a change record | Jordan Ellis | Change approval record |
| Locker custody safety | Locker Safety Owner, exercised by Sam Okafor | No standing delegation | Sam Okafor | Change approval record |
| Pickup data security and audit | Security Owner, exercised by Elena Ruiz | May delegate evidence review but not product choices | Elena Ruiz | Change approval record |

Only the named people or a delegation recorded here may accept material product
choices in their scope. Each approval names the person who acted.

## Product

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Read with | Triggers |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `PROD-PARCEL-PICKUP` | Parcel Pickup Coordinator | Accepted | `intent/product.md` | Parcel pickup behavior; pickup data security and audit | `IMPL-PICKUP-SERVICE`, `IMPL-PICKUP-SERVICE-LEGACY` | `intent/glossary.md` | parcel, locker, compartment, pickup token, controller |

## Glossaries

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Applies to |
| --- | --- | --- | --- | --- | --- | --- |
| `GLO-PARCEL-PICKUP` | Parcel pickup terms | Accepted | `intent/glossary.md` | Parcel pickup behavior | `IMPL-PICKUP-SERVICE`, `IMPL-PICKUP-SERVICE-LEGACY` | `PROD-PARCEL-PICKUP`, `CAP-PICKUP` |

## Capabilities

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Read with | Triggers |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `CAP-PICKUP` | Collect a parcel | Accepted | `intent/capabilities/CAP-PICKUP.md` | Parcel pickup behavior; locker custody safety; pickup data security and audit | `IMPL-PICKUP-SERVICE`, `IMPL-PICKUP-SERVICE-LEGACY` | `intent/glossary.md`, `intent/qualities/QLT-AUDIT.md`, `intent/decisions/DEC-0001.md` | claim, scan, pickup, open, door, timeout, retry, recovery, expire |

## Qualities

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Applies to |
| --- | --- | --- | --- | --- | --- | --- |
| `QLT-AUDIT` | Timely, secret-free pickup audit | Accepted | `intent/qualities/QLT-AUDIT.md` | Pickup data security and audit | `IMPL-PICKUP-SERVICE`, `IMPL-PICKUP-SERVICE-LEGACY` | `CAP-PICKUP` |

## Durable product decisions

| ID | Title | State | Path | Affected intent |
| --- | --- | --- | --- | --- |
| `DEC-0001` | Hold a claim while an open result is unknown | Accepted | `intent/decisions/DEC-0001.md` | `CAP-PICKUP.unknown-result-blocks-claim`, `CAP-PICKUP.retry-unknown-result`, `CAP-PICKUP.exhaustion-requires-recovery`, `CAP-PICKUP.reconcile-unknown-result` |

## Implementation targets

| ID | Name and scope | Owner | Current implementation revision | Accepted intent revision | Checkpoint | Latest evidence | Detailed record |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `IMPL-PICKUP-SERVICE` | Fictional Pickup Service 5.x release line at controller-revision-7 sites | Pickup Service team | `example-build-17` | `intent-example-17` | Conformant | `changes/CHG-20260701-CONTROLLER-UNCERTAINTY/evidence.md` | none |
| `IMPL-PICKUP-SERVICE-LEGACY` | Fictional Pickup Service 4.8 release line at older-controller sites | Legacy Pickup Service team | `build-4.8` | `intent-example-17` | Nonconformant | `changes/CHG-20260701-CONTROLLER-UNCERTAINTY/evidence-legacy.md` | none |

## Active changes

None. The latest accepted behavior change is
`changes/CHG-20260701-CONTROLLER-UNCERTAINTY/change.md`.

## Known conformance gaps

No gap is currently recorded for `IMPL-PICKUP-SERVICE` at `example-build-17`
against `intent-example-17`. This statement reports the fictional evidence
record; it does not prove that no gap exists.

| Implementation target | Intent ID | Current behavior | Tracking change | Owner | Latest evidence |
| --- | --- | --- | --- | --- | --- |
| `IMPL-PICKUP-SERVICE-LEGACY` | `CAP-PICKUP.unknown-result-blocks-claim` | Build 4.8 releases the claim after its final timeout | Not scheduled; sites must upgrade before joining the 5.x target | Legacy Pickup Service team | `changes/CHG-20260701-CONTROLLER-UNCERTAINTY/evidence-legacy.md` |
| `IMPL-PICKUP-SERVICE-LEGACY` | `CAP-PICKUP.one-request-id` | Build 4.8 uses a new request ID for each retry | Not scheduled; sites must upgrade before joining the 5.x target | Legacy Pickup Service team | `changes/CHG-20260701-CONTROLLER-UNCERTAINTY/evidence-legacy.md` |

## Retired artifacts

None.

## ID convention

This project uses semantic requirement IDs such as
`CAP-PICKUP.retry-unknown-result`. Normative scenarios append a semantic slug
to their parent requirement ID. The fictional service targets use
`IMPL-PICKUP-SERVICE` and `IMPL-PICKUP-SERVICE-LEGACY` so their different
revisions and results remain separate.
