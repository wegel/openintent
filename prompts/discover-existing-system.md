# Discover behavior in an existing system

Act as the discoverer for `<bounded product area>` in implementation target
`<IMPL-NAME>`.

## Read

1. `<nearest AGENTS.md>`
2. `<intent index and any existing intent for the area>`
3. `<named code, tests, telemetry, incidents, policies, interviews, tickets, and interface sources>`

## Goal

Answer `<concrete behavior questions>` with source-backed claims while keeping
observed, intended, unknown, and conflicting behavior separate.

## Allowed writes

- `discovery/<area>.md`
- source links and questions in `<related change record, if any>`

Do not edit accepted intent, implementation, or tests in this task.

## Method

1. Record each source with implementation target, revision, date, environment,
   what it can show, and known limits.
2. State each behavior claim concretely.
3. Label each claim only `OBSERVED`, `INTENDED`, `UNKNOWN`, or `CONFLICT`.
4. Use `INTENDED` only with product-authority evidence and an accepted intent or
   linked pending change.
5. Keep incompatible sources visible instead of averaging them into vague text.
6. Separate product states from implementation fields.
7. Turn unknown and conflicting claims into concrete alternatives with actor
   consequences.
8. Name the registered product authority that must decide each product question.

## Return

- discovery path;
- implementation target and sources inspected and not inspected;
- claims grouped by state;
- confidence and environmental limits;
- product decisions needed;
- the smallest capability boundary ready for intent authoring.
