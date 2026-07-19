# Parcel Pickup Coordinator agent guide

This file is the canonical entry point for this example.

## Authority

- Accepted branch: `main`
- Accepted product intent: `intent/`
- Intent index: `intent/index.md`
- Product authority registry: `intent/index.md#product-authority-registry`
- Implementation targets: `IMPL-PICKUP-SERVICE` and
  `IMPL-PICKUP-SERVICE-LEGACY`

Accepted intent on `main` outranks the fictional implementation evidence,
tests, discovery notes, and old changes. Report a conflict or missing rule rather
than guessing.

## Read order

1. Read `intent/index.md`.
2. Read the named change record.
3. Read only affected capabilities and linked qualities, terms, and decisions.
4. Select one implementation target and read only its fictional implementation
   material named by the change or index.

## Work rules

- Write clear pickup intent before implementation when practical.
- Update affected intent on the working branch and the active change when you
  find a product gap while implementing or testing. The same participant may
  edit intent and code.
- Ask the person registered for the affected authority scope to accept every
  material product choice discovered during implementation.
- Keep databases, queues, modules, and tasks in the change plan.
- Pause only work that would encode an unresolved product choice.
- Preserve intent IDs and record evidence by ID.
- Keep each target's checkpoint and evidence separate. Never use evidence from
  one target as proof for another.
- When a target or accepted intent revision changes, treat old evidence as stale
  and return that target to `Unknown` until current evidence supports a new
  checkpoint.
- Do not treat this example's fictional evidence as a check on the OpenIntent
  repository.

## Checks in the fictional project

- Focused checks: `parcel-harness run pickup --change CHG-20260701-CONTROLLER-UNCERTAINTY`
- Full checks: `parcel-harness run all`
- Quality exercise: `parcel-harness measure audit --profile peak-site`

These commands document the fictional evidence environment. They are not tools
included with OpenIntent.
