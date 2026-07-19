# <Quality title>

| Field | Value |
| --- | --- |
| ID | `QLT-<NAME>` |
| Status | Draft |
| Product authority scope | `<registry scope>` |
| Accepted change | `<change ID or pending>` |
| Applies to | `<capability IDs>` |
| Last reviewed | `<YYYY-MM-DD>` |

## Product reason

<!-- Name the actor and harm or outcome that requires this quality. -->

`<Actor>` needs `<measured behavior>` because `<concrete consequence>`.

## Measurement rules

<!-- Define clocks, samples, exclusions, percentile calculation, supported
environments, and other terms needed to reproduce the result. -->

- `<Measurement term>` means `<precise rule>`.

## Requirements

### QLT-<NAME>.<requirement-slug> <Measured requirement>

Under `<operating conditions>`, for `<scope>`, the `<product component>` MUST
achieve `<threshold or range>`, measured by `<method>`.

#### QLT-<NAME>.<requirement-slug>.<scenario-slug> <Boundary condition>

This scenario is normative.

- GIVEN `<workload, environment, and starting state>`
- WHEN `<measurement event or window>`
- THEN `<threshold result>`
- AND `<allowed exclusions or required failure result>`

## Assumptions

- **ASSUMPTION:** `<fact outside product control that affects measurement>`

## Unspecified observable behavior

- **UNSPECIFIED:** `<actor-visible measurement outcome that product authority
  permits implementations to vary>`

<!-- Omit unobservable measurement and implementation techniques. Delete this
section when product authority has not accepted observable variation. -->

## Acceptance map

| Intent ID | Environment and workload | Evidence needed | Review cadence |
| --- | --- | --- | --- |
| `QLT-<NAME>.<requirement-slug>` | `<declared conditions>` | `<benchmark, exercise, analysis, or inspection>` | `<when evidence becomes stale>` |
| `QLT-<NAME>.<requirement-slug>.<scenario-slug>` | `<boundary conditions>` | `<scenario check>` | `<when evidence becomes stale>` |

## Open questions

<!-- Delete before acceptance when a question affects conformance. -->

- **OPEN QUESTION:** `<question>` Owner: `<person>`. Blocks: `<ID or gate>`.
