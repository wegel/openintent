# Draft an OpenIntent change

Act as the intent author for `<change ID or proposed outcome>`.

## Read

1. `<nearest AGENTS.md>`
2. `<intent index>`
3. `<affected capability and quality paths>`
4. `<relevant discovery, issue, incident, research, or policy sources>`

Do not read unrelated capabilities or old changes unless an explicit link or a
newly found dependency requires them.

## Goal

Propose the smallest complete product-contract edit that lets `<actor>` achieve
`<outcome>` while preserving `<important invariants or existing behavior>`.

## Allowed writes

- `changes/<change-id>/change.md`
- affected files under `intent/`
- `intent/index.md` when routing changes
- a proposed durable product decision when the choice needs one

Do not edit implementation code, tests, or technical architecture in this task.

## Method

1. Classify each source claim as intended, observed, unknown, or conflicting.
2. Name product questions before drafting answers. Do not infer intended behavior
   from code or tests.
3. Define outcome, boundary, actors, permissions, non-goals, and relevant states.
4. Name the registered product-authority scope for every material product
   choice.
5. Write one observable obligation per stable ID where practical. Link every
   permission, state, transition, or flow summary that carries a product duty to
   its governing IDs.
6. Cover relevant rejection, failure, recovery, retry, concurrent, late, expiry,
   privacy, safety, accessibility, and quality behavior.
7. Apply the replaceability test to each technical detail.
8. Mark normative scenarios explicitly. Add every product invariant,
   requirement, and normative scenario to an acceptance map.
9. Summarize added, changed, retired, and preserved IDs in the change record.
10. Find active changes that touch the same IDs. Record an order, rebase point,
    or named person who will resolve each overlap.
11. Name every implementation target in scope and give each target its own
    checkpoint row. Do not copy one target's state to another.
12. Keep blocking questions visible with owners. Leave the change state `Active`
   and the intent checkpoint `Draft`.

## Return

- paths changed;
- affected and preserved intent IDs;
- blocking questions and decision owners;
- assumptions and deliberately unspecified choices;
- implementation details removed from intent;
- overlapping changes and how the project will handle them;
- current change and intent checkpoints plus each target checkpoint; and
- a short readiness statement for intent review.
