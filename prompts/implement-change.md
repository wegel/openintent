# Implement and refine an OpenIntent change

Act as the implementer for `<change ID>` and implementation target
`<IMPL-NAME>`.

## Read

1. `<nearest AGENTS.md>`
2. `<intent index>`
3. `<change record>`, its current intent checkpoint, the named target row, and
   overlapping active changes
4. `<affected capability, quality, glossary, and decision paths>`
5. `<technical project guidance>`
6. relevant implementation files found through repository search

Do not load unrelated historical changes.

## Goal

Implement every affected intent ID and normative scenario for `<IMPL-NAME>`
while preserving `<risk-adjacent IDs>`.
When you find a product gap while implementing or testing, improve proposed
intent and return material choices to product authority.

## Allowed writes

- implementation code and tests inside `<scope>`;
- affected intent on the working branch and `intent/index.md`;
- `changes/<change-id>/change.md`, including checkpoint and approval updates;
- `changes/<change-id>/plan.md`;
- `changes/<change-id>/evidence.md` with checks actually run.

Do not mark a material product edit accepted unless product authority accepted
it.

## Method

1. Confirm the target boundary and immutable starting revision. Do not infer
   another target's state from this work.
2. Map each affected ID and normative scenario to implementation work and a
   focused check.
3. Choose internal mechanics that meet accepted behavior and project technical
   rules.
4. Protect every invariant during migration and partial rollout.
5. Add or revise checks for success, rejection, failure, recovery, repeat, race,
   and quality boundaries that apply.
6. Tag each check with the most specific applicable scenario ID, or otherwise
   with the requirement or invariant ID.
7. Run focused checks after each coherent step and project-wide checks before
   handoff.
8. Record exact commands, results, environment, target, and evidence links.
9. If intent is missing, wrong, conflicting, or materially ambiguous, pause only
   dependent work, edit the proposed intent or add a concrete question, set the
   intent checkpoint to `Review required`, and ask product authority.
10. Continue independent work and use tests or prototypes to clarify open
   choices.
11. Record product discoveries separately from technical choices.
12. If the target revision or accepted intent revision changes, mark evidence
    that no longer applies and set this target's checkpoint to `Unknown` until
    current evidence supports another value.

## Return

- implementation target, starting revision, ending revision, and files changed;
- proposed intent files changed and their review state;
- intent IDs and normative scenarios completed and not completed;
- technical choices and consequences;
- checks run with exact results;
- product questions or evidence gaps;
- overlapping changes handled or still unresolved; and
- next bounded action or readiness for conformance review.
