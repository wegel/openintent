# Verify OpenIntent conformance

Act as the conformance reviewer for `<change ID>`, implementation target
`<IMPL-NAME>`, accepted intent revision `<immutable intent revision>`, and
implementation revision `<immutable implementation revision>`, target kind
`<component or composition>`, and operating profiles `<PROF IDs or none>`. Check
`<claim scope: this change's listed rules or the whole target intent scope>`.

## Read order

1. `<nearest AGENTS.md>`
2. `<affected accepted intent>`, profiles, normative references, and acceptance maps
3. `<change record>`
4. `<existing evidence record>`
5. relevant tests, implementation, and external reports
6. `<implementation plan>` last

## Goal

Determine whether named evidence supports conformance for the named target,
revisions, and claim scope. Do not fix defects unless the task separately grants
that scope.

## Allowed writes

- `changes/<change-id>/evidence.md`
- review findings in `<project review location>`

Do not edit product intent or implementation in this review.

## Method

1. List every affected product invariant, MUST, MUST NOT, SHOULD, and SHOULD NOT
   rule, plus each normative scenario and risk-adjacent invariant.
2. Map each item to a concrete check and reproducible conditions.
3. For a composition target, record every component and external participant
   revision, configuration, and role. Do not reuse component conclusions.
4. Inspect or run relevant checks. Seek negative, permission, failure, recovery,
   duplicate, race, time, and quality counterexamples.
5. Record each applicable profile revision, actual condition, and deviation.
6. For governed supporting artifacts, name the REF ID and compare only its
   normative properties under the declared variation.
7. Record `PASS`, `FAIL`, `NOT RUN`, or `INCONCLUSIVE` for every item.
8. State what each evidence item cannot prove.
9. Check every SHOULD departure for its exceptional condition, reason,
   consequences, and product acceptance.
10. Keep failed and missing evidence visible.
11. Check that every result still applies to the named target, participant,
    intent, profile, and supporting-artifact revisions. Mark stale results and
    do not use them as current proof.
12. Choose `Does not conform` when any applicable rule has `FAIL`. Otherwise
   choose `Not determined` when evidence is missing, stale, `NOT RUN`, or
   `INCONCLUSIVE`. Choose `Conforms` only when every applicable rule passes or a
   strong default has an accepted departure.

## Finding form

Give the exact intent ID, implementation location, evidence, actor-visible
consequence, and required follow-up. Separate product conformance findings from
general code-quality suggestions.

## Return

- claim scope, target kind, implementation target, intent revision,
  implementation revision, participant revisions, profiles, and environment
  checked;
- coverage summary by intent ID and normative scenario;
- failed, missing, and inconclusive evidence;
- stale evidence excluded from the conclusion;
- counterexamples attempted;
- conclusion and its limits;
- reviewer name and date.
