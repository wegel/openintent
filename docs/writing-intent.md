# Writing product intent

Good intent lets two independent implementers build observably compatible
products while still choosing different internal designs.

## Start with an outcome

Name who needs an outcome, what they can observe, and why it matters. Avoid
starting with a component to build.

Weak:

> Add a Redis queue and a retry worker.

Stronger:

> When the locker controller cannot answer, the locker service keeps an accepted
> open request and retries without asking the recipient to scan again.

The stronger statement exposes a product need. An implementer can later compare
several technical designs.

## Draw the boundary

For each capability, answer:

- Which actors can start an action?
- Which actors receive a result?
- What enters and leaves the product boundary?
- What result does the capability own?
- Which nearby result belongs to another capability or outside system?
- Which tempting features are non-goals?

A clear non-goal prevents an agent from filling the blank with plausible but
unwanted scope.

## Write one obligation at a time

A useful requirement has five parts when applicable:

1. **Actor:** a person, external system, or named product component.
2. **Trigger:** the event or state that makes the rule apply.
3. **Action:** what the actor or product does or refuses to do.
4. **Result:** what another actor can observe or what invariant remains true.
5. **Bound:** time, quantity, order, precision, or another measurable limit.

Weak:

> The platform SHOULD handle retries reliably and securely.

Stronger:

> `CAP-OPEN.retry-controller-timeout` After the controller times out, the locker service MUST retry the
> same open request no more than three times within 20 seconds and MUST reuse its
> request ID for every attempt.

The stronger version gives a reviewer one retry owner, a bound, and one request
identity that makes duplicate attempts refer to the same action.

When one sentence contains independent obligations, split it into separate IDs.
A reviewer can then pass one and fail another without an ambiguous result.

## Use scenarios to expose boundaries

A scenario should test a rule, not retell a happy-path story. Include the
initial state, event, visible result, and relevant unchanged facts.

```markdown
### CAP-PICKUP.first-valid-claim-wins One winner

The locker service MUST grant at most one pickup claim for a parcel.

#### CAP-PICKUP.first-valid-claim-wins.concurrent-submissions Concurrent valid submissions

This scenario is normative.

- GIVEN an available parcel and two valid submissions for its pickup token
- WHEN the locker service handles both submissions concurrently
- THEN exactly one submission receives a pickup claim
- AND the other submission receives a response that the token is no longer usable
- AND both responses identify the same parcel without exposing recipient data
```

Use `GIVEN`, `WHEN`, and `THEN` when the sequence helps. Use a transition table
for state machines and a timeline for timing races. The format serves the rule,
not the reverse. A normative scenario appears in the acceptance map and uses its
own ID in targeted evidence. Mark an illustrative scenario `EXAMPLE` instead.

## State models

Name product states when legal actions depend on them. Do not copy database
status fields unless those fields exactly match the product contract.

A compact state table can show:

| From | Event | To | Actor-visible result | Governing intent ID |
| --- | --- | --- | --- | --- |
| Available | First valid claim succeeds | Claimed | Winner may request the door to open | `CAP-PICKUP.first-valid-claim-wins` |
| Available | Pickup window ends | Expired | Token no longer works | `CAP-PICKUP.expire-unclaimed-assignment` |
| Claimed | Door opens | Collecting | Recipient may remove the parcel | `CAP-PICKUP.apply-open-result` |
| Claimed | Claim lease ends before open | Available | Recipient may retry with the same token | `CAP-PICKUP.release-expired-claim` |

State, permission, flow, and transition tables summarize named requirements.
They do not create product duties without governing IDs.

For every state, ask who can enter it, who can leave it, which clocks apply, and
what happens after a crash.

## Invariants

An invariant must survive every legal path, including retries, concurrent
actions, partial failures, administrative actions, and recovery.

Examples:

- A parcel has at most one active pickup claim.
- A compartment holds at most one active parcel assignment.
- A failed open command never marks a parcel collected.
- An operator cannot recover a compartment without creating an audit event.

Each invariant needs a stable ID and evidence that stresses the paths most
likely to break it.

## Failure and recovery

"Return an error" rarely specifies enough. Name:

- what failed;
- what the initiating actor observes;
- which state remains or changes;
- whether the actor can retry;
- whether the product retries automatically;
- how duplicate work is prevented;
- when retries stop;
- who can recover; and
- what audit or notification appears.

Separate rejection from failure. A rejected unauthorized request may be a fully
successful product outcome. A timeout after accepting work creates a different
recovery duty.

## Concurrent and repeated actions

For each action that can overlap or repeat, answer:

- What identifies the same logical request?
- Which action may win?
- What does each losing actor observe?
- Can actors safely retry after an unknown result?
- Which ordering rules cross devices or processes?
- Which invariant survives every order?

Avoid prescribing a lock, queue, or transaction unless an external boundary
requires one. Specify the winner and visible result.

## Permissions, privacy, and abuse

Name the actor and protected action. "Admins can manage lockers" hides too much.
State which administrator role can perform which action, which object scope it
controls, and what unauthorized callers observe.

Also ask:

- Does the response reveal that a protected object exists?
- Can a valid actor enumerate another user's objects?
- Which events require an audit record?
- Who can read that record and for how long?
- What rate or abuse boundary protects a credential or scarce resource?
- What happens when permission changes during an in-flight action?

Security words without observable rules belong in rationale, not acceptance
criteria.

## Quality requirements

Use a measurement frame:

> Under **conditions**, for **scope**, the product MUST achieve **threshold**, as
> measured by **method**.

Example:

> During a controller outage that lasts at most five minutes, 99 percent of
> accepted open requests MUST either succeed or reach the declared exhausted
> state within six minutes, measured from the service's durable acceptance time.

The requirement says which requests count, when the clock starts, which results
count, and how an outage changes expectations.

## Reuse operating conditions with profiles

When several rules repeat a substantial workload, data shape, device class,
platform range, topology, dependency set, or failure state, put those conditions
in an operating profile. Keep each actor duty and threshold in its capability or
quality rule.

For example, `PROF-PEAK-SITE` may define 500 pickup actions per second, two
service processes, regional audit contract revision 1, and a 15-minute
measurement window. `QLT-AUDIT.event-availability` still states how quickly an
audit event must become readable under that profile.

Do not put a passing result, current hardware serial number, transient host, or
implementation technique in a profile. Evidence records the actual environment
and deviations for one run.

## Use the clearest medium for exact boundary detail

Text remains the semantic anchor for actors, states, permissions, failures,
accessibility meaning, and required results. Some exact details communicate more
clearly through another medium:

- a screenshot, SVG, or interactive rendering can define visual relationships;
- an audio file can define an audible cue;
- a timing diagram can define event relationships;
- a protocol annex, schema, or fixture can define interoperable fields and
  bytes; and
- a diagram can define an externally visible topology or hardware arrangement.

Create a normative supporting-artifact record only when exact artifact content
forms part of the product boundary. The governing requirement explains why it
matters. The record states which properties are normative, which details merely
illustrate, and how platforms, viewports, languages, accessibility modes, or
protocol versions may vary.

Do not promote an implementation screenshot, generated fixture, or design
exploration merely because it exists. Product authority accepts the reference
through the normal change loop. Keep a reviewable source or rendering in Git so
no hosted editor owns the contract.

## Own shared contracts once

In a multi-product repository, place each shared protocol, user journey, data
boundary, or operator contract under one product. Consuming products link to the
owner's intent IDs and specify their own failure or compatibility behavior.
They do not paraphrase the shared rule.

When a change touches several products, one coordinator tracks the combined
work while each product authority accepts only its own scope.

## Assumptions and external dependencies

An assumption names a fact the product does not control:

> ASSUMPTION: The locker controller preserves a request ID for at least 24 hours
> and returns the prior result for a duplicate ID.

Then state what the product does when that assumption fails, if the failure is
credible and consequential. If the product must detect or compensate for the
condition, that behavior is a requirement rather than only an assumption.

## Unspecified observable choices

Use `UNSPECIFIED` only after deciding that implementations may vary safely.

Good candidates include response wording within a fixed information boundary,
presentation order that carries no semantic meaning, or retry timing anywhere
inside an accepted window.

Poor candidates include error visibility, permission boundaries, money rounding,
retry limits, data retention, and external wire formats. Those choices affect
actors or compatibility and usually need product intent.

Do not list internal storage, scheduling policy, module boundaries, algorithms,
or private log formatting as `UNSPECIFIED`. Omit them from intent. Record a
noteworthy choice in an implementation plan or technical record.

## Acceptance maps

For each normative ID, name evidence that could distinguish a conforming build
from a nonconforming build. Do not name a test file before an implementation
exists unless the path itself forms part of project policy.

| Intent ID | Evidence needed |
| --- | --- |
| `CAP-PICKUP.one-active-claim` | A controlled concurrent run that attempts two claims and inspects the final state |
| `CAP-PICKUP.retry-unknown-result` | A fault-injection run that loses controller responses and counts attempts and request IDs |
| `CAP-PICKUP.retry-unknown-result.lost-success` | A lost-success scenario that proves one request ID survives every retry |
| `QLT-RECOVERY.outage-result-time` | A timed outage exercise with the declared traffic profile and percentile calculation |

The completed evidence record later links to actual tests, reports, revisions,
and results.

## Final writer check

Before asking for intent review, confirm that:

- every noun names something a product user, operator, external system, or
  implementer can identify;
- each normative sentence contains a concrete actor and action;
- each bound has units and a clock or counting rule;
- scenarios cover rejection and recovery as well as success;
- every normative scenario and product-wide invariant has an acceptance method;
- every permission and transition summary links to governing IDs;
- examples do not create hidden rules;
- no architecture choice appears without an external reason;
- every shared contract has one owning product;
- every operating profile defines conditions without hiding a duty or result;
- every normative supporting artifact has a governing requirement, declared
  scope, allowed variation, and checked-in reviewable form;
- every open question has an owner and blocks acceptance when needed; and
- every requirement has a plausible acceptance method.
