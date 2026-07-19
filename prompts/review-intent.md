# Review proposed product intent

Act as the intent reviewer for `<change ID>`.

## Read order

1. `<nearest AGENTS.md>`
2. `<intent index>`
3. accepted versions of `<affected intent paths>`
4. the proposed Git diff for those paths
5. `<change record>`

Do not read the implementation plan before forming independent product boundary
questions.

## Goal

Find any ambiguity, omission, conflict, hidden implementation choice, or weak
acceptance method that could let two reasonable implementations differ at a
meaningful boundary.

## Review probes

- actor identity, object scope, and denied information;
- outcome boundaries and non-goals;
- creation, transition, cancellation, expiry, and terminal states;
- malformed, stale, duplicate, unauthorized, late, and concurrent actions;
- partial failure, unknown result, retry identity, exhaustion, and recovery;
- invariants across administrative and recovery paths;
- measurable privacy, security, accessibility, safety, and quality rules;
- assumptions that hide a product duty;
- material edits whose product-authority scope is missing from the registry;
- permission, state, transition, or flow summaries that state product duties
  without governing normative IDs;
- normative scenarios missing from the acceptance map;
- active changes that touch the same IDs without a recorded order, rebase point,
  or resolver;
- `UNSPECIFIED` choices that users or integrations can observe;
- technical details that fail the replaceability test; and
- acceptance methods that cannot distinguish conformance.

## Finding form

For each finding, give:

- severity: blocking, high, medium, or low;
- exact intent ID and path;
- a concrete counterexample or missing case;
- the actor-visible consequence;
- why existing text does not settle it; and
- the smallest required action.

Do not invent a finding quota. If no material issue remains, state which probes
you performed and why the proposed contract settles them.

## Authority

Suggest wording but do not accept product tradeoffs. Route each material choice
to the approver registered for `<product-authority scope>`.

## Return

- blocking findings;
- nonblocking findings;
- product decisions needed;
- authority scopes and overlapping changes checked;
- scope checked;
- review result: changes requested or ready for product acceptance.
