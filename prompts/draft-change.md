# Draft an OpenIntent change

Act as the intent author for `<change ID or proposed outcome>`.

## Read

1. `<nearest AGENTS.md>`
2. `<root index and affected product index>`
3. `<affected capability topics, quality, profile, and reference paths>`
4. `<relevant discovery, issue, incident, research, or policy sources>`

Do not read unrelated capabilities or old changes unless an explicit link or a
newly found dependency requires them.

## Goal

Propose the smallest complete product-contract edit that lets `<actor>` achieve
`<outcome>` while preserving `<important invariants or existing behavior>`.

## Allowed writes

- `changes/<change-id>/change.md`
- affected files under each registered intent root
- root or product indices when ownership or routing changes
- a proposed durable product decision when the choice needs one

Do not edit implementation code, tests, or technical architecture in this task.

## Method

1. Classify each source claim as intended, observed, unknown, or conflicting.
2. Name product questions before drafting answers. Do not infer intended behavior
   from code or tests.
3. Define outcome, boundary, actors, permissions, non-goals, and relevant states.
4. Name the registered product-authority scope for every material product
   choice.
5. For shared behavior, name one owning product and link every consumer to the
   owner's intent IDs. For a cross-product change, name one coordinator and
   every affected authority scope, then route the change from the root and each
   affected product index.
6. Write one observable obligation per stable ID where practical. Link every
   permission, state, transition, or flow summary that carries a product duty to
   its governing IDs.
7. Cover relevant rejection, failure, recovery, retry, concurrent, late, expiry,
   privacy, safety, accessibility, and quality behavior.
8. Apply the replaceability test to each technical detail.
9. Use an operating profile only for reused supported conditions. Use a
   normative supporting artifact only when exact checked-in content forms part
   of the boundary; state its governed properties and allowed variation.
10. Mark normative scenarios explicitly. Add every product invariant,
   requirement, and normative scenario to an acceptance map.
11. Summarize added, changed, retired, and preserved intent, profile, and
    reference IDs in the change record.
12. Find active changes that touch the same IDs. Record an order, rebase point,
    or named person who will resolve each overlap.
13. Name every component and composition target in scope and give each target
    its own checkpoint row. List every composition participant revision. Do not
    copy one target's state to another.
14. Keep blocking questions visible with owners. Leave the change state `Active`
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
