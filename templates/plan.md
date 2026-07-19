# Implementation plan for <change ID>

This file guides one implementation. It does not define product intent. The
current intent proposal and accepted files linked from `<change path>` control
every observable choice according to their recorded states.

| Field | Value |
| --- | --- |
| Change | `<change ID and link>` |
| Implementation target | `IMPL-<NAME>` |
| Plan owner | `<person or agent>` |
| Revision | `<date or plan revision>` |
| Status | Draft |

## Intent and scenario coverage

| Intent IDs and normative scenarios | Implementation area | Planned checks | Dependencies |
| --- | --- | --- | --- |
| `<IDs>` | `<likely modules, services, data, or interfaces>` | `<test or review approach>` | `<dependencies>` |

## Technical approach

<!-- Record architecture, algorithms, data shapes, libraries, and internal
interfaces needed for this implementation. Explain how each consequential
choice preserves an invariant or requirement. -->

<Approach>

## Technical decisions

| Decision | Reason | Consequence | Revisit when |
| --- | --- | --- | --- |
| `<choice>` | `<evidence or constraint>` | `<cost and benefit>` | `<trigger>` |

## Data and interface changes

- Data: `<migration, compatibility window, or none>`
- Internal interfaces: `<change or none>`
- External interfaces: `<must already appear in accepted intent, or none>`
- In-flight work: `<handling>`

## Work sequence

<!-- Keep tasks small enough to verify. Mark parallel work only when tasks cannot
violate a shared invariant through partial rollout. -->

1. [ ] `<task>`
   - Covers: `<intent IDs>`
   - Check: `<focused check>`
   - Depends on: `<task, outside event, or none>`

## Rollout and recovery

| Stage | Entry check | Observable result | Stop or rollback trigger | Recovery action |
| --- | --- | --- | --- | --- |
| `<stage>` | `<check>` | `<result>` | `<trigger>` | `<action and owner>` |

## Discoveries during implementation

<!-- Edit proposed intent and the change record when an implementer finds a
product need. Product authority reviews material choices. Technical discoveries
may stay here. -->

| Discovery | Kind | Action | Owner |
| --- | --- | --- | --- |
| `<fact or question>` | `<product or technical>` | `<intent review or plan update>` | `<owner>` |

## Handoff

- Completed: `<tasks and revisions>`
- Checks run: `<exact commands or linked results>`
- Open blockers: `<questions or dependencies>`
- Next action: `<one bounded action>`
