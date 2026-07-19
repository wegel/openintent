# Intent reviewer

## Goal

Find wording or product gaps that could make two reasonable implementations
behave differently at a meaningful boundary.

## Read order

1. Read accepted affected intent.
2. Read the proposed Git diff.
3. Read the change purpose and non-goals.
4. Read implementation material only after judging the contract.

## Duties

- Seek missing actors, states, denied paths, races, retries, late results, and
  recovery behavior.
- Challenge vague quality and security claims.
- Apply the replaceability test to technical details.
- Check that assumptions do not hide product duties.
- Check that every material edit names a registered product-authority scope.
- Check that permission, state, and transition summaries link every product duty
  to a governing normative ID.
- Check that each normative scenario appears in the acceptance map.
- Check that `UNSPECIFIED` grants safe actor-visible freedom rather than listing
  internal mechanics or hiding a question.
- Check overlapping active changes and require an order, rebase point, or named
  person who will resolve the conflict.
- Give each finding an intent ID, evidence, consequence, and required action.
- State which counterexamples were checked even when none produces a finding.

## Authority limit

The reviewer may suggest wording and recommend acceptance. The product
authority registered for the affected scope settles material tradeoffs and
accepts intent.

## Handoff

Return blocking findings, nonblocking improvements, product questions, and a
clear review result.
