# OpenIntent review checklist

Use the sections that match the checkpoint. Link findings to exact intent IDs
and paths. A checked box means the reviewer inspected the question, not that the
answer automatically passed.

## Intent structure

- [ ] `intent/index.md` lists every affected artifact and context link.
- [ ] The root index lists every product, product index, intent root,
  dependency, and cross-product change.
- [ ] Every shared contract has one owning product; consumers link instead of
  copying its rules.
- [ ] Each product, glossary, capability, quality, profile, reference record, and
  decision file has an ID, visible state, authority scope or decision owners,
  and linked change.
- [ ] Each operating profile and normative supporting-artifact record has an
  ID, state, authority scope, linked change, and product-index entry.
- [ ] Each modular capability index lists every normative topic and its context.
- [ ] The intent index names authority scopes, conflict resolvers, and acceptance
  records.
- [ ] Each change record has an ID, owner, state, intent checkpoint, and a
  separate row for every affected implementation target.
- [ ] Each normative requirement, invariant, and scenario has a unique ID.
- [ ] Each normative ID uses a semantic slug rather than a position number.
- [ ] Every scenario names a parent requirement.
- [ ] Every normative scenario appears in the acceptance map.
- [ ] Permission, state, flow, and transition summaries link to governing IDs.
- [ ] The change record names every added, changed, retired, and preserved
  intent, profile, and reference ID.
- [ ] Every link resolves to a repository file or durable external source.
- [ ] Every normative supporting artifact has a checked-in reviewable source or
  rendering.

## Product meaning

- [ ] A reader can identify every actor, action, object, condition, and result.
- [ ] Purpose and non-goals draw a clear boundary.
- [ ] Product terms have one meaning.
- [ ] Each normative sentence contains one obligation where practical.
- [ ] Every forbidden behavior uses `MUST NOT`.
- [ ] Examples and rationale add no hidden requirements.
- [ ] Assumptions name facts outside product control.
- [ ] `UNSPECIFIED` choices describe observable variation that product authority
  accepts.
- [ ] Unobservable internal choices stay outside intent.
- [ ] No architecture detail appears without an actor-visible, legal, safety, or
  compatibility reason.

## Behavior facets

- [ ] Actors and object scopes make permissions explicit.
- [ ] Unauthorized actions state both result and protected information.
- [ ] States and legal transitions cover creation through terminal states.
- [ ] Repeated and concurrent actions name winners, losers, and preserved
  invariants.
- [ ] Retry rules name request identity, owner, limit, exhaustion, and recovery.
- [ ] Failures state visible results and resulting state.
- [ ] Cancellation, expiry, and late results have defined behavior where relevant.
- [ ] Privacy, abuse, accessibility, safety, and audit rules appear where relevant.
- [ ] Quality rules name conditions, scope, threshold, units, and measurement.
- [ ] Operating profiles contain reproducible conditions and no hidden duty or
  passing result.
- [ ] Supporting-artifact records distinguish governed properties,
  illustrative details, and allowed variation.

## Intent acceptance

- [ ] Every blocking open question has an accepted answer.
- [ ] The canonical intent files contain each accepted answer.
- [ ] A named person or agent with product authority accepted the IDs and
  assumptions.
- [ ] The authority registry grants that approver the required scope.
- [ ] The change record gives the proposed revision, accepted IDs, approver,
  result, and date.
- [ ] Migration, compatibility, rollout, and recovery effects are explicit.

## Implementation review

- [ ] The plan maps every affected ID to work and checks.
- [ ] Internal choices remain inside accepted product freedom.
- [ ] Implementers updated proposed intent when tests or working code exposed a
  product gap.
- [ ] Product authority reviewed each material product edit discovered during
  implementation.
- [ ] Overlapping active changes name a coordinator and acceptance order.
- [ ] When accepted intent leads implementation, the index and change record
  name each target, pending owner, current behavior, revisions, and evidence.
- [ ] Only work that depended on an unresolved product choice paused.
- [ ] Partial rollout cannot violate a product invariant.
- [ ] Tests target product boundaries, not only internal functions.

## Evidence review

- [ ] The evidence record names an immutable implementation revision.
- [ ] The evidence record names one implementation target.
- [ ] The evidence record identifies the target as a component or composition.
- [ ] A composition record names every participant revision, configuration, and
  role and does not borrow a component's conclusion.
- [ ] The evidence record names the accepted intent revision.
- [ ] The evidence record names every applicable profile and records actual
  conditions and deviations.
- [ ] The evidence record says whether it covers one change or the whole target
  intent scope.
- [ ] Automated evidence includes the requirement ID in the test name or an
  adjacent comment.
- [ ] The environment and important conditions are reproducible.
- [ ] Every affected MUST and MUST NOT rule has a result row.
- [ ] Every affected normative scenario has a result row.
- [ ] Every affected SHOULD or SHOULD NOT rule passed or has an accepted
  departure.
- [ ] MAY choices still satisfy all other rules.
- [ ] Negative, permission, failure, recovery, repeat, and race paths were tested
  where relevant.
- [ ] Each result links to a concrete artifact and states its limits.
- [ ] Evidence for a governed supporting artifact names its REF ID, comparison
  conditions, governed properties, and allowed variation.
- [ ] Failed, missing, and inconclusive checks remain visible.
- [ ] The reviewer checked whether intent, code, dependencies, conditions, or
  contradictory observations made the evidence stale.
- [ ] The reviewer checked whether participant, profile, or supporting-artifact
  revisions made composition or artifact evidence stale.
- [ ] The conclusion does not claim more than the evidence shows.
- [ ] An intent-index `Conformant` checkpoint has current evidence for every
  accepted rule that applies to that target, not merely one change's rules.
- [ ] The reviewer name and date are present.

## Findings

| Severity | Intent ID or path | Finding | Evidence | Required action |
| --- | --- | --- | --- | --- |
| `<blocking, high, medium, or low>` | `<reference>` | `<specific issue>` | `<why the issue is real>` | `<edit, decision, check, or none>` |

## Review result

- Result: `<accepted, changes requested, does not conform, or not determined>`
- Reviewed by: `<name>`
- Date: `<YYYY-MM-DD>`
- Notes: `<scope and material limits>`
