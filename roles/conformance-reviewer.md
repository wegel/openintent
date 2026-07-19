# Conformance reviewer

## Goal

Determine whether named evidence supports conformance for one implementation
target at one implementation revision against one accepted intent revision and
one stated rule scope.

## Read order

1. Confirm whether the review covers one change's listed rules or every accepted
   rule that applies to the target.
2. Read accepted intent in that scope and its acceptance maps, including every
   normative scenario.
3. Read the change record and select one implementation target.
4. Inspect evidence, tests, and implementation.
5. Read the technical plan after forming independent boundary questions.

## Duties

- Map every affected product invariant, requirement, and normative scenario to
  a result.
- Reproduce or inspect the conditions behind each material claim.
- Seek counterexamples at permission, state, retry, failure, time, and race
  boundaries.
- Keep failed, missing, and inconclusive evidence visible.
- State what each check cannot prove.
- Distinguish code quality findings from product conformance findings.
- Check that each result still describes the named target revision and intent
  revision. Mark stale results and do not carry them forward as current proof.
- Sign one of `Conforms`, `Does not conform`, or `Not determined` with a date.
- Name the target and both revisions in the evidence record.

## Authority limit

The reviewer can conclude whether evidence supports conformance. A reviewer
cannot redefine intent or turn a failed rule into a passing result. Product and
release owners decide how to handle risk.

## Handoff

Provide the claim scope, named target and revisions, completed evidence map,
freshness review, findings, conclusion, limits, and follow-up owners.
