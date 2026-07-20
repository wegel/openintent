# Evidence for <change ID> and <implementation target>

| Field | Value |
| --- | --- |
| Change | `<change ID and link>` |
| Implementation target | `IMPL-<NAME>` |
| Target kind | `<component or composition>` |
| Intent revision | `<immutable accepted-branch commit>` |
| Implementation revision | `<immutable commit, build ID, digest, or composition manifest>` |
| Operating profiles | `<PROF IDs and accepted revisions, or none>` |
| Reviewer | `<person or agent>` |
| Review date | `<YYYY-MM-DD>` |
| Environment | `<versions, configuration, hardware, data, and relevant services>` |
| Conclusion | Not determined |

## Composition participants

<!-- Required for a composition target. Delete for a component target. -->

| Target or external system | Exact revision | Configuration or role | Evidence boundary |
| --- | --- | --- | --- |
| `<participant>` | `<immutable revision>` | `<relevant configuration>` | `<what this participant supplies>` |

## Scope

- Claim scope: `<this change's listed rules or the whole target intent scope>`
- Affected intent: `<invariant, requirement, and normative scenario IDs>`
- Preserved intent checked for regression: `<risk-adjacent IDs>`
- Excluded checks and reason: `<none or explicit list>`

## Evidence map

<!-- Use PASS, FAIL, NOT RUN, or INCONCLUSIVE. Keep every affected invariant,
requirement, normative scenario, and strong default visible. Each automated check
includes its most specific intent ID in the test name or an adjacent comment.
Group IDs only when the same check, conditions, result, and limits apply to each
one. -->

| Intent ID | Supporting reference | Check | Conditions and profile deviations | Result | Evidence link | Limits |
| --- | --- | --- | --- | --- | --- | --- |
| `<ID>` | `<REF ID or none>` | `<test, inspection, analysis, exercise, or observation>` | `<environment, input, profile, and deviations>` | `<result>` | `<path, report, run, screenshot, or durable URL>` | `<what this does not prove>` |

## Commands and results

<!-- Include exact commands when they help reproduction. Summarize output and
link large logs. -->

### <Check name>

```text
<command or manual procedure>
```

Result: `<exit status, measured value, observed result, and artifact link>`

## SHOULD departures

<!-- Delete when none. A permanent departure usually calls for an intent edit. -->

| Intent ID | Exceptional condition | Chosen behavior | Reason and consequences | Accepted by |
| --- | --- | --- | --- | --- |
| `<ID>` | `<condition>` | `<behavior>` | `<why and cost>` | `<person and date>` |

## Failed, missing, stale, or inconclusive evidence

<!-- Never hide a gap by removing its row. If no rule has FAIL, a missing,
stale, NOT RUN, or INCONCLUSIVE applicable rule forces Not determined. Any FAIL
forces Does not conform even when other rows remain unknown. -->

| Intent ID | Gap | Consequence | Owner | Follow-up |
| --- | --- | --- | --- | --- |
| `<ID>` | `<failed, stale, not run, or inconclusive check>` | `<what remains unknown or nonconforming>` | `<owner>` | `<change or date>` |

## Freshness review

- Applicable intent or normative terms changed: `<no, or IDs>`
- Implementation moved from the named revision: `<no, or revision>`
- Composition participant revisions changed: `<not applicable, no, or details>`
- Operating profiles or normative supporting artifacts changed: `<no, or IDs>`
- Dependencies, configuration, data, or conditions changed: `<no, or details>`
- Incidents or observations contradict this result: `<no, or links>`

## Reviewer probes

- Negative and unauthorized paths checked: `<summary>`
- Failure and recovery paths checked: `<summary>`
- Concurrent or repeated actions checked: `<summary or not relevant with reason>`
- Data and privacy effects checked: `<summary>`
- Quality conditions reproduced: `<summary or not relevant>`

## Conclusion

Choose one:

- `Conforms`
- `Does not conform`
- `Not determined`

Every conclusion records limits. A limit narrows the claim; it cannot hide a
required condition that evidence did not establish.

Reason: `<tie the conclusion to the evidence map without overstating it>`

Reviewed by: `<name>` on `<YYYY-MM-DD>`
