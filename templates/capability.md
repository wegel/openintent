# <Capability title>

| Field | Value |
| --- | --- |
| ID | `CAP-<NAME>` |
| Status | Draft |
| Product authority scope | `<registry scope>` |
| Accepted change | `<change ID or pending>` |
| Last reviewed | `<YYYY-MM-DD>` |
| Read with | `<linked glossary sections, qualities, decisions, or adjacent capabilities>` |

## Outcome and boundary

<!-- Name the actor-visible outcome and what this capability owns. -->

`<Actor>` can `<outcome>`. This capability begins when `<boundary event>` and
ends when `<terminal result>`. `<Adjacent capability or external system>` owns
`<excluded responsibility>`.

### Non-goals

- **NON-GOAL:** `<plausible behavior intentionally outside this capability>`

## Actors and permissions

<!-- Delete no relevant actor. This table summarizes named requirements below;
it cannot create an untagged product duty. -->

| Actor | Allowed summary | Forbidden summary | Scope | Governing intent IDs |
| --- | --- | --- | --- | --- |
| `<actor>` | `<actions>` | `<forbidden actions>` | `<objects or tenancy boundary>` | `<requirement IDs>` |

## Terms

<!-- Link shared terms. Define only capability-local terms here. -->

- **<term>:** `<precise local meaning>`

## State model

<!-- Keep this section when legal actions depend on product state. These are
product states, not database enum values. -->

| State | Meaning | Entry | Exit | Governing intent IDs |
| --- | --- | --- | --- | --- |
| `<state>` | `<actor-visible or invariant-relevant meaning>` | `<legal entry events>` | `<legal exit events>` | `<requirement IDs>` |

### Legal transitions

| From | Event and conditions | To | Actor-visible result | Governing intent ID |
| --- | --- | --- | --- | --- |
| `<state>` | `<event>` | `<state>` | `<result>` | `<requirement ID>` |

## Invariants

### CAP-<NAME>.<invariant-slug> <Invariant title>

The `<concrete product component>` MUST `<condition that survives every legal
path>`.

## Requirements

### CAP-<NAME>.<requirement-slug> <Requirement title>

<!-- Write one observable obligation. Name actor, trigger, action, result, and a
bound where applicable. -->

When `<condition>`, the `<actor or product component>` MUST `<observable action
or constraint>`.

#### CAP-<NAME>.<requirement-slug>.<scenario-slug> <Boundary scenario>

This scenario is normative.

- GIVEN `<initial state and relevant facts>`
- WHEN `<actor event>`
- THEN `<observable result>`
- AND `<relevant state or unchanged invariant>`

### CAP-<NAME>.<forbidden-behavior-slug> <Forbidden behavior>

The `<actor or product component>` MUST NOT `<forbidden observable behavior>`.

#### CAP-<NAME>.<forbidden-behavior-slug>.<negative-scenario-slug> <Negative scenario>

This scenario is normative.

- GIVEN `<initial state>`
- WHEN `<invalid, stale, repeated, concurrent, or unauthorized event>`
- THEN `<safe result>`
- AND `<information that remains hidden or state that remains unchanged>`

<!-- Add requirements for relevant failure, recovery, permission, privacy,
concurrency, ordering, time, expiry, cancellation, accessibility, and lifecycle
behavior. Organize around rules instead of keeping empty concern headings. -->

## Assumptions and external dependencies

- **ASSUMPTION:** `<fact outside this capability's control>`
- This capability depends on `<external system>` providing `<boundary behavior>`
  under `<contract link>`.

<!-- If this capability must detect or compensate when an assumption fails, add
a normative requirement above. -->

## Unspecified observable behavior

- **UNSPECIFIED:** `<actor-visible behavior that product authority permits
  implementations to vary>`

<!-- Omit unobservable storage, architecture, scheduling, module, and algorithm
choices from intent. Do not list them here. Delete this section when product
authority has not accepted any observable variation. -->

## Acceptance map

| Intent ID | Evidence needed |
| --- | --- |
| `CAP-<NAME>.<invariant-slug>` | `<check that stresses paths likely to break the invariant>` |
| `CAP-<NAME>.<requirement-slug>` | `<check and conditions that distinguish conformance>` |
| `CAP-<NAME>.<requirement-slug>.<scenario-slug>` | `<boundary check for the normative scenario>` |
| `CAP-<NAME>.<forbidden-behavior-slug>` | `<negative check>` |
| `CAP-<NAME>.<forbidden-behavior-slug>.<negative-scenario-slug>` | `<negative boundary check for the normative scenario>` |

## Examples

<!-- Examples are non-normative. Delete when they add no clarity. -->

- **EXAMPLE:** `<concrete input and result that illustrates a requirement>`

## Open questions

<!-- Resolve or deliberately mark safe choices UNSPECIFIED before acceptance.
Keep active questions in the change record, then delete this section. -->

- **OPEN QUESTION:** `<question>` Owner: `<person>`. Blocks: `<IDs or gate>`.
