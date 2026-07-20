# <Operating profile title>

| Field | Value |
| --- | --- |
| ID | `PROF-<NAME>` |
| Status | Draft |
| Product | `PROD-<NAME>` |
| Product authority scope | `<registry scope>` |
| Accepted change | `<change ID or pending>` |
| Applies to targets | `<IMPL IDs>` |
| Last reviewed | `<YYYY-MM-DD>` |

## Purpose

`<Actor>` needs reviewers to reproduce `<supported condition>` because
`<concrete consequence>`.

## Conditions

| Dimension | Required value or range | How a reviewer identifies it |
| --- | --- | --- |
| Workload | `<requests, actions, streams, or events>` | `<counter or fixture>` |
| Data scale | `<objects, bytes, shape, or distribution>` | `<dataset record>` |
| Device or platform | `<class, version range, or capability>` | `<system record>` |
| Topology | `<participants and links>` | `<deployment record>` |
| Dependencies | `<named contract revisions or ranges>` | `<manifest or response>` |
| Starting state | `<warm, cold, degraded, recovering, or other state>` | `<observable check>` |

Delete irrelevant rows and add concrete dimensions that the product needs.

## Allowed tolerances and exclusions

- `<dimension>` may vary from `<value>` through `<value>`.
- Exclude `<condition>` because `<product reason>`.

## Related contracts

- Governing rules: `<intent IDs that apply under this profile>`
- Base or adjacent profiles: `<profile IDs or none>`
- External contracts: `<links or none>`

## Review notes

This profile defines conditions, not product duties or passing results. Evidence
must record the actual conditions and every deviation.

