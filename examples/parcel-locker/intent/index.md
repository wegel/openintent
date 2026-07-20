# Parcel locker repository intent index

| Field | Value |
| --- | --- |
| Repository | Parcel locker products |
| OpenIntent version | `0.1` |
| Accepted branch | `main` |
| Last reviewed | 2026-07-20 |

This file routes readers to the smallest useful context set. It does not
restate requirements.

## Products

| Product ID | Title | Product index | Intent root | Authority scope | Implementation targets | Depends on | Triggers |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `PROD-PARCEL-PICKUP` | Parcel Pickup Coordinator | `intent/index.md` | `intent/` | Parcel pickup behavior; locker custody safety; pickup data security and audit | `IMPL-PICKUP-SERVICE`, `IMPL-PICKUP-SERVICE-LEGACY`, `IMPL-PICKUP-SITE-R7` | None | parcel, locker, compartment, pickup token, controller |
| `PROD-COURIER-CONSOLE` | Courier Console | `products/courier-console/intent/index.md` | `products/courier-console/intent/` | Courier exception work; courier data access | `IMPL-COURIER-PHONE`, `IMPL-COURIER-DESKTOP` | `PROD-PARCEL-PICKUP`; fulfillment system | courier, expired parcel, route stop, removal |

## Shared and cross-product contracts

| Contract | Owning product | Governing intent IDs | Consuming products | Compatibility or failure consequence |
| --- | --- | --- | --- | --- |
| Expired assignment status and data boundary | `PROD-PARCEL-PICKUP` | `PROD-PARCEL-PICKUP.secret-boundary`, `PROD-PARCEL-PICKUP.actor-scope`, `CAP-PICKUP.expire-unclaimed-assignment` | `PROD-COURIER-CONSOLE` | The draft Courier Console must preserve the pickup product's meaning of `Expired` and cannot infer an interface or new fields from that meaning |

## Product authority registry

| Scope | Authority | May delegate | Conflict resolver | Acceptance record |
| --- | --- | --- | --- | --- |
| Parcel pickup behavior | Parcel Operations Product Owner, exercised by Jordan Ellis | May delegate named IDs in a change record | Jordan Ellis | Change approval record |
| Locker custody safety | Locker Safety Owner, exercised by Sam Okafor | No standing delegation | Sam Okafor | Change approval record |
| Pickup data security and audit | Security Owner, exercised by Elena Ruiz | May delegate evidence review but not product choices | Elena Ruiz | Change approval record |

Only the named people or a delegation recorded here may accept material product
choices in their scope. Each approval names the person who acted.

The Courier Console keeps its separate registry in
`products/courier-console/intent/index.md#product-authority-registry`.

## Product

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Read with | Triggers |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `PROD-PARCEL-PICKUP` | Parcel Pickup Coordinator | Accepted | `intent/product.md` | Parcel pickup behavior; pickup data security and audit | `IMPL-PICKUP-SERVICE`, `IMPL-PICKUP-SERVICE-LEGACY`, `IMPL-PICKUP-SITE-R7` | `intent/glossary.md` | parcel, locker, compartment, pickup token, controller |

## Glossaries

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Applies to |
| --- | --- | --- | --- | --- | --- | --- |
| `GLO-PARCEL-PICKUP` | Parcel pickup terms | Accepted | `intent/glossary.md` | Parcel pickup behavior | `IMPL-PICKUP-SERVICE`, `IMPL-PICKUP-SERVICE-LEGACY`, `IMPL-PICKUP-SITE-R7` | `PROD-PARCEL-PICKUP`, `CAP-PICKUP` |

## Capabilities

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Read with | Triggers |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `CAP-PICKUP` | Collect a parcel | Accepted | `intent/capabilities/CAP-PICKUP.md` | Parcel pickup behavior; locker custody safety; pickup data security and audit | `IMPL-PICKUP-SERVICE`, `IMPL-PICKUP-SERVICE-LEGACY`, `IMPL-PICKUP-SITE-R7` | `intent/glossary.md`, `intent/qualities/QLT-AUDIT.md`, `intent/profiles/PROF-PEAK-SITE.md`, `intent/references/REF-CONTROLLER-OPEN-V7.md`, `intent/decisions/DEC-0001.md` | claim, scan, pickup, open, door, timeout, retry, recovery, expire |

## Qualities

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Applies to |
| --- | --- | --- | --- | --- | --- | --- |
| `QLT-AUDIT` | Timely, secret-free pickup audit | Accepted | `intent/qualities/QLT-AUDIT.md` | Pickup data security and audit | `IMPL-PICKUP-SERVICE`, `IMPL-PICKUP-SERVICE-LEGACY`, `IMPL-PICKUP-SITE-R7` | `CAP-PICKUP` |

## Operating profiles

| ID | Title | Intent state | Path | Authority scope | Applies to targets | Governing intent |
| --- | --- | --- | --- | --- | --- | --- |
| `PROF-PEAK-SITE` | Peak parcel site audit load | Accepted | `intent/profiles/PROF-PEAK-SITE.md` | Pickup data security and audit | `IMPL-PICKUP-SERVICE`, `IMPL-PICKUP-SERVICE-LEGACY`, `IMPL-PICKUP-SITE-R7` | `QLT-AUDIT.event-availability` |

## Normative supporting artifacts

| ID | Title | Intent state | Record | Source | Authority scope | Governing intent |
| --- | --- | --- | --- | --- | --- | --- |
| `REF-CONTROLLER-OPEN-V7` | Controller revision 7 open request | Accepted | `intent/references/REF-CONTROLLER-OPEN-V7.md` | `intent/references/controller-open-v7.json` | Locker custody safety | `CAP-PICKUP.start-open-request`, `CAP-PICKUP.one-request-id`, `PROD-PARCEL-PICKUP.secret-boundary` |

## Durable product decisions

| ID | Title | State | Path | Affected intent |
| --- | --- | --- | --- | --- |
| `DEC-0001` | Hold a claim while an open result is unknown | Accepted | `intent/decisions/DEC-0001.md` | `CAP-PICKUP.unknown-result-blocks-claim`, `CAP-PICKUP.retry-unknown-result`, `CAP-PICKUP.exhaustion-requires-recovery`, `CAP-PICKUP.reconcile-unknown-result` |

## Implementation targets

| ID | Kind | Name and scope | Owner | Components or relationships | Current revision | Accepted intent revision | Checkpoint | Latest evidence |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `IMPL-PICKUP-SERVICE` | Component | Fictional Pickup Service 5.x release line | Pickup Service team | Included in `IMPL-PICKUP-SITE-R7` | `example-build-17` | `intent-example-17` | Conformant | `changes/CHG-20260701-CONTROLLER-UNCERTAINTY/evidence.md` |
| `IMPL-PICKUP-SERVICE-LEGACY` | Component | Fictional Pickup Service 4.8 release line | Legacy Pickup Service team | Older controllers outside the revision 7 composition | `build-4.8` | `intent-example-17` | Nonconformant | `changes/CHG-20260701-CONTROLLER-UNCERTAINTY/evidence-legacy.md` |
| `IMPL-PICKUP-SITE-R7` | Composition | One pickup site using controller contract revision 7 and regional audit search | Site Integration team | `IMPL-PICKUP-SERVICE@example-build-17`; physical locker controller with model and firmware not selected, contract revision 7; regional audit implementation not selected, contract revision 1 | Not assembled | `intent-example-17` | Unknown | None |

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
| `IMPL-PICKUP-SITE-R7` | All accepted `PROD-PARCEL-PICKUP`, `CAP-PICKUP`, and `QLT-AUDIT` IDs | No evidence checks the service, physical controller, and regional audit interface as one assembled site | Assemble the fictional site and record composition evidence | Site Integration team | None |

## Retired artifacts

None.

## ID convention

This project uses semantic requirement IDs such as
`CAP-PICKUP.retry-unknown-result`. Normative scenarios append a semantic slug
to their parent requirement ID. Profiles use `PROF-`, supporting artifacts use
`REF-`, and products use `PROD-`. Each component and composition has its own
`IMPL-` ID so their revisions and results remain separate.
