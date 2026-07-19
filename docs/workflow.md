# Iterative change workflow

OpenIntent asks teams to write clear intent before implementation when they can.
It also expects implementers to find missing needs, constraints, and product
choices while they build and test. Teams move between intent, code, and evidence
until the product contract and each affected implementation target are ready for
review.

The method records authority in artifacts and names each approver. It does not
force separate phases, sessions, agents, or pull requests.

## Classify the request

Start by naming the kind of work:

| Class | Intent edit | Change record | Evidence |
| --- | --- | --- | --- |
| New or changed product behavior | Required | Required | Required before a conformance claim |
| Code does not match accepted intent | None when the rule already exists | Project policy decides | Required |
| Internal change with the same boundary behavior | None | Project policy decides | Existing checks plus risk-based evidence |
| Product exploration | Draft intent may evolve with the prototype | Required when the team is considering a product choice | Findings, not a conformance claim |
| Existing-system discovery | None until product authority decides | Required when an accepted choice follows | Discovery sources |
| Emergency safety, security, or availability fix | May follow code briefly | Required | Required, with gaps stated |

If a dependency or architecture change alters errors, latency, permissions,
retention, compatibility, or another actor-visible result, treat it as a product
behavior change.

## Track intent and each target separately

Each active change tracks intent review once and implementation work once per
target:

| Checkpoint | Typical movement |
| --- | --- |
| Intent | Draft to Partially accepted or Accepted; back to Review required when implementers find a material product edit; then Accepted again |
| Each implementation target | Not started to Exploring or In progress; then Evidence ready and Conformant, or a visible Nonconformant or Unknown state |

These checkpoints do not form a one-way state machine. A failed test, prototype,
hardware limit, or user finding can send the work back to intent review.

A change target row reports the result for that change's affected and preserved
IDs. The intent index reports the whole target scope. Maintainers copy a
`Conformant` result to the index only when current evidence covers every accepted
rule that the index applies to that target.

## 1. Route a small context set

Read the nearest `AGENTS.md`, then use `intent/index.md` to choose affected
capabilities. Follow only the glossary, qualities, decisions, and adjacent
capabilities linked from those rows.

Check active changes for the same intent IDs and normative terms. When work
overlaps, link the changes and record which proposed revision must be accepted
first.

Read relevant intent before searching code when practical. This order helps a
participant distinguish the product contract from one implementation’s
accidental behavior.

Record the context paths in `change.md` when another participant may continue
the work.

## 2. Create or update the change record

Choose a stable change ID, such as `CHG-20260718-PICKUP-RETRY`, and create:

```text
changes/CHG-20260718-PICKUP-RETRY/
  change.md
```

State why the current contract does not serve the product, which outcome may
change, and which outcomes must remain true. Name affected IDs even before the
wording becomes final.

Set:

- Change state: `Active`
- Intent checkpoint: `Draft`

Add one implementation-target row for each affected target. Set each checkpoint
to `Not started`, `Exploring`, `Unknown`, or another honest value.

Keep questions explicit. A question that can change visible behavior,
permissions, money, safety, compatibility, or acceptance results blocks product
acceptance for the affected work.

## 3. Draft the clearest current intent

Authors should edit `intent/product.md`, capabilities, qualities, glossary
entries, and durable decisions before implementation when practical. This work
gives implementers a product boundary and gives reviewers concrete choices to
challenge.

Authors edit canonical intent and the change record on the same working branch
when practical. They do not paste a second copy of each requirement into
`change.md`; Git already shows the exact edit.

A team may repeat drafting and review as many times as the product needs before
an implementer starts work. The method does not force the team into technical
work after one intent review.

When a rule changes materially:

- keep the ID when clearer wording preserves the same duty;
- add a semantic ID when the product adds a distinct duty; and
- retire and replace an ID when old and new duties need different evidence or
  could independently pass.

Update the intent index when files, context links, checkpoints, evidence links,
or trigger words change.

## 4. Review and accept product choices

An intent reviewer reads the proposed contract and asks about missing actors,
states, negative paths, races, permission leaks, quality bounds, assumptions,
and evidence methods.

Product authority records each accepted material choice in `change.md`:

```text
Intent accepted by: Morgan Lee
Date: 2026-07-19
Proposed revision: 4e6c0ab
Scope: CAP-PICKUP.retry-unknown-result,
       CAP-PICKUP.reconcile-unknown-result.late-success,
       QLT-RECOVERY.outage-result-time
```

The change sets its intent checkpoint to `Accepted` only when product authority
accepted every material choice in that proposed revision. It uses `Partially
accepted` when the approval covers only a named subset.

A team may begin technical exploration before this checkpoint. The branch must
label the product intent as draft, and reviewers cannot call the exploratory
build conformant.

## 5. Explore, implement, test, and revise

Implementers choose internal mechanics and map each affected intent ID to work
and focused checks for a named implementation target. They may edit affected
intent on the working branch and the change record when they find a product gap.

The same person or agent may write intent, code, tests, plans, and evidence when
repository scope permits. The team does not need a ceremonial role switch.
Product authority still accepts material product choices.

When work exposes a discovery:

1. Name the concrete fact, source, and actor-visible consequence.
2. Classify it as a product choice, technical finding, evidence gap, or
   observation about existing behavior.
3. Edit the artifact that owns it.
4. Set the intent checkpoint to `Review required` when the proposed edit changes
   product meaning.
5. Ask product authority to review the material edit.
6. Continue work that does not depend on the open choice.
7. Return the checkpoint to `Accepted` after the owner accepts the revised
   intent.

The implementer pauses only work that would encode an unresolved product
choice. The implementer may prepare prototypes, tests, or proposed wording that
helps product authority decide.

## 6. Keep technical work outside intent

Create `plan.md` when the change spans components, needs migration or rollout
steps, carries meaningful risk, or will pass between implementers.

The plan may choose a language, framework, module, table, queue, algorithm, or
library. Those choices guide one implementation. They enter product intent only
when an external consumer, regulator, safety property, or compatibility promise
requires them.

Do not list omitted internal mechanics as `UNSPECIFIED`. Use that label only
when product authority accepts more than one actor-visible result.

## 7. Build the evidence record

Create one evidence record for each target that reaches `Evidence ready`. Name
all three:

- the implementation target;
- the accepted intent revision; and
- the exact implementation revision.

List every affected invariant, requirement, normative scenario, and strong
default. Link each item to a concrete result and record `PASS`, `FAIL`, `NOT
RUN`, or `INCONCLUSIVE`.

Each automated check used as evidence includes its most specific intent ID in the
test name or an adjacent comment. A normative scenario check uses the scenario
ID. Include negative, failure, recovery, repeated, concurrent, and quality paths
where the contract names them.

Run checks in an environment that matches the claim. A unit test cannot prove a
percentile under production traffic. A simulated controller cannot prove
unknown firmware behavior.

## 8. Review conformance

The conformance reviewer reads:

1. the named accepted intent revision;
2. the change record;
3. the evidence table and linked results;
4. relevant implementation and tests;
5. the named implementation target and revision; and
6. the technical plan last.

The reviewer checks every applicable invariant, requirement, and normative
scenario. The reviewer checks the recorded reason and consequences for every
`SHOULD` or `SHOULD NOT` departure.

Before choosing a conclusion, the reviewer checks whether intent, implementation,
dependencies, conditions, or contradictory observations made prior evidence
stale. When no applicable rule failed, a stale or missing applicable result
forces `Not determined`.

For high-risk money, safety, permission, privacy, or irreversible-data changes,
the project should use a reviewer who did not choose the implementation.

## 9. Accept, continue, or leave implementation pending

Maintainers may choose any honest result for each target:

- accept a target revision as conforming to the change scope and complete the
  change when no other work remains;
- continue another intent and implementation loop;
- accept intent while implementation remains not started or in progress;
- record a known nonconforming implementation; or
- withdraw the change and say why.

When accepted intent leads implementation, the intent index and active change
record name each target, intent revision, implementation revision and checkpoint,
currently deployed behavior when it differs, owner, and latest evidence.

A reader should never need to infer implementation state from an intent file.
Accepted means “the product requires this,” not “all current code already does
this.”

After completion, the change directory stays at its stable path. Git supplies
history, while the stable path preserves links from decisions and evidence.

## 10. Learn from operation

Telemetry, incidents, support reports, user research, and replacement
implementations may show that the contract is wrong or incomplete. They supply
evidence for another loop. They do not edit intent by implication.

## Review depth by risk

Projects should scale review effort with real consequences:

| Risk | Suggested practice |
| --- | --- |
| Low, easily reversible copy or display behavior | One author, one reviewer, focused checks |
| Moderate state or integration behavior | Intent review, failure scenarios, integration evidence, recovery step |
| High money, safety, permission, privacy, or irreversible-data behavior | Named product authority, independent conformance reviewer, race and fault probes, staged rollout, recovery exercise |

Every risk level uses the same vocabulary. Reviewers change depth, not the
artifact model.
