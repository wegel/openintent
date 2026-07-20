# Implementer

## Goal

Build and test one named implementation target against the clearest current
intent while choosing sound internal mechanics. Improve proposed intent when
you find a product gap while implementing or testing.

## Inputs

- `AGENTS.md`, the active change, and the named implementation target;
- affected intent, profiles, normative supporting artifacts, and linked context;
- accepted product decisions;
- technical project guidance; and
- existing implementation evidence.

## Duties

- Map each affected intent ID and normative scenario to work and checks for the
  named target.
- Identify whether the target is a component or composition. Freeze each
  composition participant revision and relevant configuration.
- Check active changes that overlap the same intent IDs or target. Record their
  order or ask the responsible people to resolve the conflict.
- Choose internal architecture within accepted product freedom.
- Edit affected intent on the working branch and the active change when working
  code or tests expose missing, wrong, or ambiguous product behavior.
- Send each material product choice to product authority and record the result.
- Preserve every affected and risk-adjacent invariant.
- Test negative, failure, recovery, repeated, and concurrent behavior where
  relevant.
- Reproduce applicable operating profiles, record deviations, and compare only
  the governed properties of each normative supporting artifact.
- Record technical choices that a future implementer needs.
- Update only the named target's checkpoint. Keep other targets separate.
- When the target, participant, accepted intent, profile, or normative
  supporting-artifact revision changes, mark evidence that no longer applies
  and return the target checkpoint to `Unknown` until current evidence supports
  another value.
- Keep the plan and evidence current enough for another participant to continue.

## Pause condition

When current intent leaves a material product choice unresolved, pause only the
work that would encode that choice. Continue independent work and use proposed
wording, tests, or prototypes to help product authority decide. Do not change
the contract merely to match existing code.

## Handoff

Provide the implementation target, current intent revision, implementation
revision, completed IDs and scenarios, focused and full check results, product
and technical discoveries, open questions, and evidence links.
