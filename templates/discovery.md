# Discovery: <area>

This file stages evidence about an existing system. It does not define product
intent.

| Field | Value |
| --- | --- |
| Area | `<bounded product or implementation area>` |
| Implementation target | `IMPL-<NAME>` |
| Revision | `<commit, release, build, or unknown>` |
| Environment | `<configuration, hardware, data, or unknown>` |
| Discoverer | `<person or agent>` |
| Date | `<YYYY-MM-DD>` |
| Related change | `<change ID or none>` |

## Questions being investigated

- `<Concrete product behavior question>`

## Source inventory

| Source | Target, revision, or date | What it can show | Limits |
| --- | --- | --- | --- |
| `<code, test, trace, interview, policy, ticket, or document link>` | `<target and revision, or date>` | `<supported claim type>` | `<why it may be incomplete or stale>` |

## Claims

Use only `OBSERVED`, `INTENDED`, `UNKNOWN`, or `CONFLICT`.

| Claim | State | Evidence | Confidence and limits | Next step |
| --- | --- | --- | --- | --- |
| `<concrete behavior>` | `OBSERVED` | `<source and location>` | `<conditions and uncertainty>` | `<product question or check>` |
| `<confirmed behavior>` | `INTENDED` | `<product authority plus intent or pending change link>` | `<scope>` | `<evidence or none>` |
| `<unanswered behavior>` | `UNKNOWN` | `<sources searched>` | `<what remains missing>` | `<source or decision owner>` |
| `<incompatible claims>` | `CONFLICT` | `<source A>; <source B>` | `<conditions for each>` | `<person who must decide>` |

## State or flow observed

<!-- Optional. Label every diagram or table OBSERVED and name the source. Do not
copy it into intent without product review. -->

| From | Event | To | Evidence |
| --- | --- | --- | --- |
| `<state>` | `<event>` | `<state>` | `<source>` |

## Product decisions needed

| Question with alternatives | Consequence | Product owner | Needed by |
| --- | --- | --- | --- |
| `<question>` | `<how implementations or actors would differ>` | `<person>` | `<gate or date>` |

## Promotion record

<!-- Record claims moved into accepted intent through a normal change. -->

| Discovery claim | Intent ID | Change | Accepted by and date |
| --- | --- | --- | --- |
| `<claim>` | `<ID>` | `<change link>` | `<person, YYYY-MM-DD>` |
