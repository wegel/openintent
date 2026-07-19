# Intent index

| Field | Value |
| --- | --- |
| Product | `<name>` |
| OpenIntent version | `0.1` |
| Accepted branch | `<branch>` |
| Contract state | Draft |
| Last reviewed | `<YYYY-MM-DD>` |

This file routes readers to the smallest useful context set. It does not restate
requirements.

## Product authority registry

| Scope | Authority | May delegate | Conflict resolver | Acceptance record |
| --- | --- | --- | --- | --- |
| `<product or intent-ID scope>` | `<person, group, role, or policy>` | `<person or policy and limits>` | `<person>` | `<change approval table or durable system>` |

The person or agent who exercises a role or applies a policy records their name
or stable agent identity in each change. A policy-based approval also names the
policy revision. An agent has product authority only when this registry grants
it for the exact scope.

## Product

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Read with | Triggers |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `PROD-<NAME>` | `<product title>` | Draft | `intent/product.md` | `<registry scope>` | `IMPL-<NAME>` | `<glossary or none>` | `<product-wide search terms>` |

## Glossaries

<!-- Delete this section until the product needs a shared or product-wide
glossary. Capability-local terms may stay in their capability. -->

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Applies to |
| --- | --- | --- | --- | --- | --- | --- |
| `GLO-<NAME>` | `<product or domain glossary>` | Draft | `intent/glossary.md` | `<registry scope>` | `IMPL-<NAME>` | `<product and capability IDs>` |

## Capabilities

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Read with | Triggers |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `CAP-<NAME>` | `<actor outcome>` | Draft | `intent/capabilities/CAP-<NAME>.md` | `<registry scope>` | `IMPL-<NAME>` | `<term, quality, decision, or adjacent capability paths>` | `<request words, events, or objects>` |

## Qualities

<!-- Delete this section until the first cross-cutting quality file exists. -->

| ID | Title | Intent state | Path | Authority scope | Implementation targets | Applies to |
| --- | --- | --- | --- | --- | --- | --- |
| `QLT-<NAME>` | `<measured quality>` | Draft | `intent/qualities/QLT-<NAME>.md` | `<registry scope>` | `IMPL-<NAME>` | `<capability IDs>` |

## Durable product decisions

<!-- Decision records explain rules but do not create them. Delete this section
until a durable decision exists. -->

| ID | Title | State | Path | Affected intent |
| --- | --- | --- | --- | --- |
| `DEC-0001` | `<decision title>` | Draft | `intent/decisions/DEC-0001.md` | `<intent IDs>` |

## Implementation targets

| ID | Name and scope | Owner | Current implementation revision | Accepted intent revision | Checkpoint | Latest evidence | Detailed record |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `IMPL-<NAME>` | `<service, application, device, or release line>` | `<person or team>` | `<immutable revision or not started>` | `<accepted Git commit or pending>` | Not started | `<evidence link or none yet>` | `<path or none>` |

Never combine targets whose revisions or conformance results differ.
Use `Conformant` here only when current evidence covers every accepted rule that
this index applies to the target. Link an evidence collection when several
records provide that coverage.

## Active changes

| ID | Owner | Change state | Intent checkpoint | Proposed intent revision | Affected intent | Implementation targets | Overlaps | Path |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `CHG-<DATE>-<NAME>` | `<person>` | Active | Draft | `<working-branch commit or pending>` | `<IDs>` | `<IMPL IDs or not applicable>` | `<change IDs and order, or none>` | `changes/CHG-<DATE>-<NAME>/change.md` |

## Known conformance gaps

<!-- List accepted intent that an implementation target does not yet satisfy.
An empty table means no known gaps, not proof that none exist. -->

| Implementation target | Intent ID | Current behavior | Tracking change | Owner | Latest evidence |
| --- | --- | --- | --- | --- | --- |
| `IMPL-<NAME>` | `<intent ID>` | `<observed behavior>` | `<change link>` | `<person or team>` | `<failed, stale, inconclusive, or absent evidence>` |

## Retired artifacts

<!-- Keep every retired ID findable. Delete this section until needed. -->

| ID | Former title | Tombstone path | Replacement or removing change |
| --- | --- | --- | --- |
| `<retired ID>` | `<title>` | `<stable path>` | `<replacement ID or change>` |

## ID convention

- Product: `PROD-<NAME>`
- Capability: `CAP-<NAME>`
- Glossary: `GLO-<NAME>`
- Invariant or requirement: `CAP-<NAME>.<semantic-slug>`
- Scenario: `CAP-<NAME>.<parent-slug>.<scenario-slug>`
- Quality requirement: `QLT-<NAME>.<semantic-slug>`
- Decision: `DEC-<four digits>`
- Change: `CHG-<YYYYMMDD>-<NAME>`
- Implementation target: `IMPL-<NAME>`

Never reuse a retired ID for a different meaning.
