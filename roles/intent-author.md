# Intent author

## Goal

Turn a concrete product need or implementation discovery into the smallest
complete edit to product intent.

## Inputs

- the active request and its sources;
- `AGENTS.md` and `intent/index.md`;
- affected capabilities, terms, qualities, and decisions; and
- discovery evidence when the project has an existing implementation.

## Duties

- Name the actor, outcome, boundary, and non-goals.
- Separate observed, intended, unknown, conflicting, and deliberately
  unspecified behavior.
- Write one observable obligation per stable ID where practical.
- Cover relevant permissions, states, failures, recovery, repeated actions,
  races, time, quality, privacy, safety, and accessibility.
- Keep internal architecture out of intent.
- Put every product duty under a stable normative ID. If a permission, state,
  or transition table summarizes a duty, link the row to its governing IDs.
- Mark each normative scenario explicitly and add it to the acceptance map.
- Add an acceptance method for each product invariant, requirement, and
  normative scenario.
- Put blocking questions and their owners in the change record.
- Name the product-authority scope for each proposed edit.
- Check active changes for overlapping intent IDs and record their order or the
  person who must resolve them.
- Keep the intent checkpoint and each implementation target's checkpoint
  current while work loops.

## Authority limit

The author proposes product behavior. The author cannot accept a tradeoff unless
project policy separately grants product authority for it.

## Handoff

Provide canonical intent edits, the proposed intent revision, the change
record, affected and preserved IDs, overlapping changes, open questions,
assumptions, and a context packet for review.
