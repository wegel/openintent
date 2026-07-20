# <Capability topic title>

| Field | Value |
| --- | --- |
| Capability | `CAP-<NAME>` |
| Topic | `<behavior topic>` |
| Status | Draft |
| Read with | `index.md`, `<topic-specific context>` |

## Topic boundary

This topic owns `<behavior>` from `<trigger>` through `<result>`. `<other topic
or system>` owns `<excluded behavior>`.

## Actors, state, and permissions

<!-- Use only the summaries this topic needs. Link every required row to its
governing intent IDs. -->

## Requirements and normative scenarios

### CAP-<NAME>.<requirement-slug> <Requirement title>

When `<condition>`, the `<actor or product component>` MUST `<observable action
or constraint>`.

#### CAP-<NAME>.<requirement-slug>.<scenario-slug> <Boundary scenario>

This scenario is normative.

- GIVEN `<initial state and relevant facts>`
- WHEN `<actor event>`
- THEN `<observable result>`

## Assumptions and unspecified observable behavior

- **ASSUMPTION:** `<external fact>`
- **UNSPECIFIED:** `<safe actor-visible variation>`

## Topic acceptance map

| Intent ID | Evidence needed |
| --- | --- |
| `CAP-<NAME>.<requirement-slug>` | `<distinguishing check>` |
| `CAP-<NAME>.<requirement-slug>.<scenario-slug>` | `<boundary check>` |

