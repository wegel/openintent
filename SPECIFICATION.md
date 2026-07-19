# OpenIntent 0.1

Status: Pre-publication draft  
Last updated: 2026-07-19  
License: MIT

Maintainers update this pre-publication draft in place. It MUST remain version
0.1 through its first public release; draft edits change the last-updated date,
not the version number.

## Abstract

OpenIntent defines a Markdown and Git method for treating product intent as the
authoritative source for software development. People and coding agents write,
review, implement, and test a product contract in short, repeated loops.

Teams SHOULD write clear intent before implementation when they can. Teams MAY
also revise intent while they implement and test, because working software often
reveals missing needs, constraints, failures, and product choices. OpenIntent
keeps those revisions explicit without treating code as product authority.

This document defines conformance. Guides, templates, prompts, roles, and
examples explain these rules but do not override them.

## 1. Normative words and labels

OpenIntent uses uppercase **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and
**MAY** with the meanings defined by
[BCP 14](https://www.rfc-editor.org/info/bcp14/). Lowercase forms carry their
ordinary meanings.

- **MUST** and **MUST NOT** set absolute conformance rules.
- **SHOULD** and **SHOULD NOT** set strong defaults. A project may depart when
  maintainers understand and record the reason and consequences.
- **MAY** permits a choice.

OpenIntent also uses these labels. They do not set requirement strength.

- **NON-GOAL:** The product deliberately excludes this outcome from the stated
  scope.
- **ASSUMPTION:** The author believes this external fact to be true, but the
  product does not control it.
- **UNSPECIFIED:** Product authority deliberately permits more than one
  actor-visible outcome and accepts implementations that choose differently.
- **OPEN QUESTION:** Named product authority must settle this product choice
  before the affected intent can become accepted.
- **RATIONALE:** This text explains a rule but does not add a rule.
- **EXAMPLE:** This text illustrates a rule but does not add a rule.

Authors MUST NOT list unobservable internal mechanics as `UNSPECIFIED`. They
normally omit those mechanics from intent. An implementation plan or technical
record may preserve a noteworthy internal choice.

Authors MUST NOT use `ASSUME`, `PREFER`, or `UNRESOLVED` as requirement levels.
Authors use `ASSUMPTION` for an external fact, `SHOULD` for a preferred product
behavior, `OPEN QUESTION` for an undecided product choice, and `UNSPECIFIED`
only when product authority accepts observable variation.

### 1.1 Core terms

- **Product intent:** The accepted product, glossary, capability, and quality
  files that state what actors may observe and what the product must preserve.
- **Normative rule:** An invariant, requirement, or normative scenario that can
  change a conformance result. A rule carries a semantic intent ID.
- **Observable:** Detectable by a user, operator, external system, regulator, or
  conformance check at a product boundary. Internal state may count when a
  named safety, audit, recovery, or legal rule depends on it.
- **Product authority:** A named person, agent, group, role, or policy that
  repository rules empower to accept product choices for an explicit scope.
  Each acceptance record names the person or agent who exercised or applied
  that authority.
- **Material product choice:** A choice that can change observable behavior,
  permissions, money, safety, privacy, accessibility, compatibility, a quality
  threshold, or the result of a conformance check.
- **Accepted intent revision:** An immutable Git commit on the accepted branch
  that contains the accepted intent used for a product or conformance claim.
- **Proposed intent revision:** An immutable working-branch commit submitted for
  product review. It does not become authoritative until product authority
  accepts the relevant choices and maintainers merge it to the accepted branch.
- **Implementation target:** A stable named implementation, such as one service,
  application, device build, or supported release line, whose revisions can be
  checked against intent. Target IDs use `IMPL-<NAME>` by default.
- **Implementation revision:** An immutable commit, build identifier, image
  digest, or equivalent identifier for one implementation target.
- **Evidence scope:** One implementation target and revision checked against one
  accepted intent revision under named conditions.
- **Preserved intent:** An unchanged rule that a change could plausibly break
  and that reviewers therefore include in regression evidence. It does not mean
  every unaffected rule in the product.

## 2. Authority

### 2.1 Accepted branch

An OpenIntent project MUST name one Git branch as its accepted branch. The
project SHOULD use its default branch. `AGENTS.md` MUST name a different branch
when the project does not use the default branch.

On the accepted branch, accepted product, glossary, capability, and quality files
under `intent/` define product intent. Code, tests, telemetry, tickets, chat,
plans, old changes, discovery notes, and decision rationale do not override those
files.

Only an accepted product-intent artifact on the accepted branch is authoritative.
Draft files and edits on another branch are proposals. An accepted artifact
edited on a working branch may keep its `Accepted` lifecycle state; that state
does not accept the branch edits. The active change record carries the review
checkpoint for those edits.

### 2.2 Product authority registry

Each project MUST keep a product authority registry in `intent/index.md` or link
one from that file. For each scope, the registry MUST name:

- the person, group, role, or policy that may accept product choices;
- the person or policy that may delegate a narrower choice;
- the person who resolves overlapping or disputed scopes; and
- the durable place where reviewers record acceptance.

Each product, glossary, capability, and quality artifact MUST name its authority
scope or link to the matching registry entry. A change record MUST name each
person or agent who exercised that authority; a role name alone does not
identify who accepted a particular revision. When a registry entry derives
authority from a policy, the acceptance record MUST also identify the policy and
revision that the named approver applied.

An agent MUST NOT claim product authority unless the registry explicitly grants
that agent authority for the exact choice.

### 2.3 Conflict rules

A project MUST apply these rules when sources disagree:

1. The conflict resolver named in the product authority registry resolves a
   conflict between accepted intent files. Agents report the conflict and do not
   invent precedence.
2. A change record explains an edit but does not override the edited intent
   file.
3. A decision record explains why maintainers chose a policy but does not create
   a requirement by itself.
4. A scenario, rationale, or example cannot weaken or expand its parent
   requirement.
5. Code and tests show what one implementation does. They do not decide what the
   product should do.
6. A discovery record may show observed behavior, but product authority MUST
   accept that behavior before an intent file can require it.

### 2.4 Intent and implementation states

Each product, glossary, capability, quality, and decision artifact MUST show one
of these states:

| Intent state | Meaning |
| --- | --- |
| Draft | Reviewers may discuss the file, but implementers cannot treat it as an accepted product rule |
| Accepted | The file forms part of the product contract on the accepted branch |
| Retired | The file serves as a tombstone and points to its replacement or removing change |

A change record MUST track intent review and each affected implementation target
separately:

| Field | Allowed values |
| --- | --- |
| Change state | Active, Completed, Withdrawn |
| Intent checkpoint | Draft, Partially accepted, Accepted, Review required |
| Implementation checkpoint | Not started, Exploring, In progress, Evidence ready, Conformant, Nonconformant, Unknown, Not applicable |

Projects MAY add states when `AGENTS.md` defines them. A state label does not
replace the named reviewer, date, revision, target, or recorded result.

An intent checkpoint applies to one proposed intent revision:

- `Draft` means product authority has not accepted any material choice in that
  revision.
- `Partially accepted` means product authority accepted a recorded subset of IDs
  while other material choices remain open.
- `Accepted` means product authority accepted every material choice that the
  change proposes in that exact revision.
- `Review required` means an edit or conflicting accepted change made an earlier
  review result stale.

Each implementation checkpoint applies to one implementation target, one
implementation revision when it exists, and one intent revision. `Conformant`
means current evidence concludes `Conforms`; `Nonconformant` means current
evidence concludes `Does not conform`; and `Unknown` means no current evidence
supports either conclusion. `Evidence ready` means the implementer has supplied
evidence for review but no reviewer has issued a current conclusion.

Every implementation checkpoint MUST make its intent scope clear. In a change
record, the checkpoint covers the affected and preserved rules that the record
lists. In the intent index, a `Conformant` checkpoint covers every accepted rule
that the index applies to that target. A project MUST NOT copy a change-scoped
`Conformant` result into the intent index unless current evidence, taken
together, covers every accepted rule that applies to the target. The index MAY
link an evidence collection instead of one record when several records supply
that coverage.

A change reaches `Completed` only when its record has no required work left. If
the change still owns pending implementation work, it remains `Active`. A project
MAY complete an intent-only change with each target marked `Not applicable` and
track later implementation in a linked change; the intent index still shows each
target's current conformance state.

An accepted intent file MAY describe behavior that no implementation target has
shipped yet. The intent index and active change record MUST show that gap for
each affected target. Reviewers MUST NOT call a target and revision conformant
until evidence covers that target, implementation revision, and intent revision.

An implementation MAY temporarily lead proposed intent while the team explores a
product need. The branch and change record MUST keep the affected edits marked as
proposals, and product authority MUST accept every material product choice before
reviewers call the implementation target and revision conformant.

## 3. Replaceability test

Intent files describe required outcomes and observable boundaries. Authors
SHOULD leave internal mechanics to implementers.

Before adding a technical detail, an author asks:

> Could another implementation meet every user, operator, legal, and external
> interface need without using this detail?

If yes, the author SHOULD leave the detail out of accepted intent. An
implementation plan or technical record MAY keep it instead.

An intent file MAY name a protocol, data format, algorithm, dependency, or
technology when a consumer, regulator, safety property, compatibility promise,
or other product boundary requires that exact choice. The file MUST state the
observable reason.

## 4. Required artifacts

### 4.1 Agent entry point

Each project MUST keep `AGENTS.md` at its repository root. That file MUST:

- state that accepted intent outranks implementation evidence;
- name the accepted branch;
- point to the product authority registry;
- point to the intent index and active change records;
- give agents a short read order;
- tell agents to report conflicting or missing intent instead of guessing;
- tell agents how the project runs relevant checks; and
- point to nested `AGENTS.md` files in a monorepo.

`AGENTS.md` SHOULD route readers instead of copying full specifications.

A project MAY add vendor-specific adapter files. Each adapter MUST point to
`AGENTS.md` and MUST NOT introduce product rules.

### 4.2 Intent index

`intent/index.md` MUST list every product, glossary, capability, quality, and
durable decision artifact on the accepted branch, including Draft and Retired
artifacts. Each entry MUST give:

- the stable artifact ID, title, path, and intent state; and
- the other files a reader needs with it.

Each product, glossary, capability, and quality entry MUST also give the
implementation targets to which it applies.

Unless a narrower normative rule says otherwise, every rule in an artifact
applies to every implementation target listed for that artifact.

The index MUST contain or link the product authority registry. It MUST also list
each implementation target with its owner, current implementation revision,
accepted intent revision, implementation checkpoint, and latest evidence. A
project with many targets MAY keep detailed target records outside `intent/` and
link them from the index.

The index MUST keep retired artifact IDs findable and point to their replacements
or removing changes.

The index SHOULD include search terms or change triggers so an agent can choose
a small context set without reading every intent file.

### 4.3 Product intent

`intent/product.md` MUST state:

- the product purpose and outcomes;
- actors outside the implementation;
- the product boundary and non-goals;
- system-wide invariants;
- the capability map; and
- product-wide assumptions or dependencies.

The product file MUST give each product-wide invariant a semantic ID and MUST
include an acceptance map for those invariants.

The product file SHOULD stay short. Detailed behavior belongs in capability or
quality files.

### 4.4 Capability intent

Each coherent product ability MUST have a capability file under
`intent/capabilities/`. A capability file MUST include:

- a stable capability ID and intent state;
- the outcome and boundary;
- relevant actors and permissions;
- every invariant that the capability owns;
- normative requirements with stable semantic IDs;
- scenarios that make important requirements observable;
- assumptions and external dependencies;
- deliberately unspecified observable choices, when any exist; and
- an acceptance map that names the evidence needed for each requirement.

A capability file MUST cover relevant failure, recovery, permission, privacy,
concurrency, ordering, time, and lifecycle behavior. Writers MAY organize these
concerns around requirements instead of keeping empty sections.

Only these parts of a capability create normative product duties:

- an invariant or requirement under a semantic ID heading that uses a normative
  BCP 14 word; and
- a scenario whose semantic ID extends a parent requirement ID and that the file
  explicitly treats as normative.

Actor, permission, state, flow, and transition tables summarize the contract.
Each row that describes required behavior MUST link to the semantic IDs that
create that duty. A table row without such an ID link MUST NOT create a product
duty. Writers use `EXAMPLE` for illustrative scenarios.

Writers MUST express forbidden behavior with a `MUST NOT` requirement. An
informal forbidden example does not set a product rule by itself.

### 4.5 Quality intent

Cross-cutting quality rules MUST live under `intent/qualities/` when they apply
to more than one capability or would otherwise repeat. Each quality requirement
MUST name:

- the measured behavior;
- the operating conditions;
- the threshold or allowed range;
- the scope; and
- the evidence that can demonstrate the result.

Words such as “fast,” “secure,” “reliable,” and “accessible” do not form a
testable requirement by themselves.

Each normative quality scenario MUST appear in the quality acceptance map.

### 4.6 Glossary

Projects MUST define product terms that a reasonable reader could interpret in
more than one way. A project MAY define a capability-local term in that
capability. It SHOULD keep shared or product-wide terms in one or more glossary
files under `intent/`.

Each glossary file MUST carry a stable glossary ID, intent state, accepted
change, and product authority scope. Each term entry SHOULD state the exact
meaning, allowed aliases, terms to avoid, and the intent artifacts that use it.

Large projects MAY split domain terms into several glossary files. The intent
index MUST route readers to each file.

### 4.7 Change record

Every change that alters accepted product intent MUST keep a stable record under
`changes/<change-id>/change.md`. The record MUST state:

- why the product needs the change;
- the intended outcome and non-goals;
- each added, changed, retired, and preserved intent ID;
- compatibility, migration, release, and recovery effects;
- assumptions and open questions;
- the change state and intent checkpoint;
- who accepted each material product choice and when;
- the proposed and accepted intent revisions when those revisions exist; and
- each affected implementation target, its owner, checkpoint, implementation
  revision, current deployed behavior, and latest evidence.

The acceptance record MUST identify the proposed intent revision, accepted IDs,
result, named approver, and date. When product authority accepts only some
proposed IDs, the change MUST use `Partially accepted` and keep the remaining
choices visible.

Before a participant edits an intent ID, that participant MUST check active
changes for the same ID. Overlapping changes MUST link to each other, name one
owner who coordinates acceptance order, and state which proposed revision builds
on the other. If another accepted change alters an affected rule or normative
term, the later change MUST rebase and return its intent checkpoint to `Review
required` unless product authority confirms that the prior acceptance still
applies.

A project that accepts its first intent MUST use one baseline change record. For
an existing system, baseline acceptance does not claim implementation
conformance; each target begins as `Unknown`, `Nonconformant`, or another honest
checkpoint backed by evidence.

The same working branch SHOULD edit the canonical intent files that the record
names. The record summarizes those edits and MUST NOT copy their full normative
text. Git supplies the exact delta.

A change MAY keep `plan.md` for technical work. The plan does not define product
intent. A change MUST keep a current evidence record for each target before
reviewers call that target conformant. One evidence record covers one target and
revision; a change that affects several targets keeps them in separate records.

Completed change directories stay at their stable paths. Projects MUST NOT move
them into an archive directory. Git records time; stable paths preserve links.

### 4.8 Evidence record

An evidence record MUST identify:

- the change, implementation target, intent revision, and implementation
  revision;
- the environment and important test conditions;
- each affected invariant, requirement, and normative scenario, including every
  `MUST`, `MUST NOT`, `SHOULD`, and `SHOULD NOT` rule;
- a concrete test, inspection, analysis, or observed result for each item;
- `PASS`, `FAIL`, `NOT RUN`, or `INCONCLUSIVE` for each item;
- known limits, deviations, and items not checked; and
- the reviewer and review date.

An evidence record MAY link to test files, logs, reports, screenshots, or
external systems. It SHOULD summarize results and link large outputs.

A passing test suite MUST NOT serve as proof for requirements it does not
exercise.

An evidence record MUST conclude exactly one of:

- `Conforms`: every applicable invariant, requirement, and normative scenario
  has `PASS`, except that a strong default may have an accepted departure;
- `Does not conform`: at least one applicable invariant, requirement, or
  normative scenario has `FAIL`, even when other applicable rules have missing
  or inconclusive results; or
- `Not determined`: no applicable invariant, requirement, or normative scenario
  has `FAIL`, but missing, stale, `NOT RUN`, or `INCONCLUSIVE` evidence prevents
  `Conforms`.

Every conclusion MUST record limits. A limit narrows the stated evidence scope;
it MUST NOT hide a required condition that the check did not establish. A
release owner MAY accept operational risk, but that choice MUST NOT turn `Does
not conform` or `Not determined` into `Conforms`.

Current evidence becomes stale when:

- an accepted edit changes an applicable rule or normative term;
- the implementation target moves to a different behavior-relevant revision;
- a dependency, configuration, data shape, or environment leaves the checked
  conditions; or
- an incident or observation contradicts the recorded result.

When evidence becomes stale, the target checkpoint MUST move from `Conformant`
or `Nonconformant` to `Unknown` until a reviewer evaluates current evidence. Old
evidence records remain at stable paths and keep their original scope.

### 4.9 Decision record

A project MAY keep durable product decisions under `intent/decisions/`. A
decision record captures context, the chosen policy, alternatives,
consequences, affected intent IDs, and a review trigger. Its `Accepted` state
means the named approvers accepted that account of the decision; it does not
make the record normative product intent.

A decision record does not replace normative text. When the chosen policy
changes product behavior, the same change MUST update a capability or quality
requirement.

Implementers SHOULD keep internal architecture choices outside `intent/`, such
as in a change plan or a project-specific technical record.

### 4.10 Discovery record

A project that studies an existing implementation MAY keep records under
`discovery/`. Each claim MUST use one of these states:

- **OBSERVED:** Named evidence shows this behavior in a named revision or
  environment.
- **INTENDED:** Product authority confirmed this behavior, and an accepted
  intent file contains it or a linked active change proposes it.
- **UNKNOWN:** Available evidence cannot answer the question.
- **CONFLICT:** Named sources support incompatible answers.

An agent MUST NOT promote `OBSERVED` to `INTENDED`. Product authority accepts
that choice through the normal change loop.

## 5. Default project layout

A conforming project SHOULD use this layout:

```text
AGENTS.md
intent/
  index.md
  product.md
  glossary.md
  capabilities/
    CAP-<NAME>.md
  qualities/
    QLT-<NAME>.md
  decisions/
    DEC-<NUMBER>.md
changes/
  CHG-<DATE>-<NAME>/
    change.md
    plan.md
    evidence.md
discovery/
  <area>.md
implementations/
  IMPL-<NAME>.md
```

`intent/glossary.md`, `plan.md`, `intent/decisions/`, `discovery/`, and detailed
`implementations/` records are optional. An evidence record is required only
before a reviewer calls an implementation target conformant. The intent index
still lists every implementation target. A small project MAY begin with one
capability and add files only when a real product need calls for them.

A project MAY use different paths when existing repository rules require them.
Its root `AGENTS.md` MUST map each OpenIntent artifact type to the actual path.

For a monorepo, the root intent index SHOULD route readers to product-level
indices. Each independently owned product MAY keep its own nested `AGENTS.md`,
`intent/`, and `changes/` directories. The nearest `AGENTS.md` applies while
root rules still constrain the whole repository.

## 6. IDs, links, tests, and Git

### 6.1 Semantic IDs

Each product, glossary, capability, quality, and durable decision artifact MUST
have an ID. Each invariant, requirement, and normative scenario MUST also have
an ID. Writers MAY revise a proposed ID; after product authority accepts the
artifact or rule, writers MUST keep its ID stable. Projects SHOULD use these
forms:

```text
PROD-PARCEL-PICKUP
GLO-PARCEL-PICKUP
CAP-PICKUP
CAP-PICKUP.one-active-claim
CAP-PICKUP.retry-unknown-controller-result
CAP-PICKUP.retry-unknown-controller-result.lost-success
QLT-AUDIT.event-availability
DEC-0001
CHG-20260718-LOCK-RETRY
IMPL-PICKUP-SERVICE
```

Artifact IDs use an uppercase type prefix. Requirement and invariant IDs append
a lowercase kebab-case slug that names the behavior, not its position. A
normative scenario appends another semantic slug to its parent requirement ID.

Projects MAY use another unambiguous convention, but the intent index MUST
document it.

Writers MUST NOT reuse a retired ID for a different meaning. An intent ID names
one continuing behavioral duty, not one exact sentence or threshold. Writers
keep the ID when the same actor and duty gain clearer wording, changed
conditions, or a revised bound. The accepted intent revision identifies which
version of that duty evidence covers.

Writers retire and replace an ID when a duty splits or combines, moves to a
different actor, changes into a different outcome, or would otherwise make old
and new evidence appear to test the same duty when they do not. The change record
links every retired and replacement ID.

### 6.2 Links

Each trace link MUST use an ID plus a repository path or durable external link.
Line numbers MAY help a review but MUST NOT serve as the only reference.

### 6.3 Test tags

Each automated check that serves as conformance evidence MUST include the most
specific applicable intent ID verbatim in its test name or an adjacent comment.
A check for a normative scenario uses the scenario ID. Projects MAY choose the
language-specific syntax.

```text
test("one claim wins a token race [CAP-PICKUP.first-valid-claim-wins]")
```

A test MUST NOT pin behavior that intent deliberately marks `UNSPECIFIED`.

### 6.4 Git trailers

Commits that change accepted intent or implement named requirements SHOULD carry
standard Git trailers:

```text
Change: CHG-20260718-LOCK-RETRY
Implements: CAP-PICKUP.retry-unknown-controller-result
```

Projects that squash commits SHOULD preserve these trailers in the final commit.
Projects MAY use another durable Git convention when `AGENTS.md` explains it.

## 7. Requirement and scenario form

Each requirement MUST name a concrete actor or product component, an observable
action or constraint, and the conditions that make it apply.

Each requirement SHOULD contain one obligation so evidence can return one clear
result. Writers MAY keep tightly coupled effects together when one product
action cannot satisfy them independently.

Scenarios SHOULD use `GIVEN`, `WHEN`, and `THEN` when that form makes a rule
clear. Writers MAY use tables, state transitions, timelines, examples, or prose
when those forms describe behavior more precisely.

Each normative scenario MUST sit under or link to a parent requirement. A
scenario MAY narrow conditions or expose an edge case. It MUST NOT create an
unrelated obligation.

A file MUST state whether its scenarios are normative. Every normative scenario
MUST appear in the acceptance map and in evidence when a change affects it.

Writers mark non-normative examples with `EXAMPLE`.

Stateful capabilities SHOULD name states and legal transitions. Requirements
that face concurrent actions SHOULD state which outcome may win, what each loser
observes, and which invariant survives every order.

Requirements that retry work SHOULD name the logical request, retry owner,
exhaustion result, time bounds, and recovery path.

## 8. Iterative change loop

### 8.1 Intent leads, then learns

Teams SHOULD write enough clear intent to guide implementation before they begin
the implementation loop. When teams write intent first, they expose product
choices while those choices are cheap to change.

A team MAY revise and review intent through any number of drafts before an
implementer starts work. OpenIntent does not require a draft to enter an
implementation loop after one review.

Teams MUST expect implementation, testing, prototypes, operations, and user
feedback to reveal missing or incorrect intent. Authors MAY revise proposed intent
and implementation together in the same branch, pull request, or working
session.

OpenIntent defines responsibilities and authority. It does not require separate
people, agents, sessions, or sequential phases.

### 8.2 The loop

Projects MUST use these recurring checkpoints for work that can affect product
behavior:

1. **Classify.** The participant identifies an intent change, conformance fix,
   internal change, exploration, or existing-system discovery.
2. **Route.** The participant reads `AGENTS.md`, the intent index, affected
   files, linked terms and qualities, overlapping active changes, and no
   unrelated context unless needed.
3. **Record.** The participant creates or updates a change record when the work
   proposes a product choice.
4. **Draft intent.** The author writes the clearest current product contract and
   exposes open questions. The team SHOULD do this before implementation when
   practical.
5. **Review intent.** A reviewer checks boundaries, permissions, states,
   failures, concurrent actions, qualities, assumptions, and evidence methods.
   Product authority accepts material product choices.
6. **Explore, implement, and test.** Implementers choose internal mechanics and
   build against the clearest current intent. They MAY edit affected intent on
   the working branch and the change record when the work exposes a gap.
7. **Revisit intent.** The team classifies each discovery and updates the
   correct artifact. Material product edits return to intent review. Technical
   choices stay in the plan or technical records. Observations about existing
   code stay in discovery until accepted.
8. **Verify.** A reviewer maps each applicable invariant, requirement, and
   normative scenario to concrete evidence, probes forbidden and failure
   behavior, and records limits.
9. **Accept or continue.** Maintainers MAY accept the current implementation
   target and revision, continue another loop, leave accepted intent pending
   implementation, or withdraw the change.
10. **Learn.** Operators and users MAY supply new evidence. A new product choice
    starts or resumes the loop.

The loop may revisit any earlier checkpoint. A change record MUST show the
current intent checkpoint and a separate checkpoint for each implementation
target so another reader can continue without relying on chat history.

### 8.3 Discoveries during implementation

When a participant finds a new fact while implementing or testing, that
participant classifies it:

| Discovery | Required action |
| --- | --- |
| Product behavior is missing, wrong, or ambiguous | Edit proposed intent and the change record; seek product review for a material choice |
| A technical approach fails but the product contract remains sound | Update the plan or technical record; choose another approach |
| Existing code behaves unexpectedly | Record evidence or discovery; do not copy the behavior into intent automatically |
| A requirement cannot be tested as written | Revise the requirement or evidence method through intent review |
| A quality target appears infeasible | Record the result and let product authority revise, retain, or reject the target |

The same person or agent MAY edit intent and code when repository scope permits.
No participant needs an artificial role switch. Product authority still MUST
accept material product choices.

An implementer MUST pause only the work that would encode an unresolved product
choice. The implementer MAY continue independent work and MAY prepare proposed
intent wording, tests, or prototypes that help the owner decide.

### 8.4 Accepted intent before implementation

A project MAY accept intent before any implementation begins. A project MAY
also merge accepted intent while its implementation remains incomplete.

For each affected implementation target, the intent index and active change
record MUST name:

- the accepted intent revision;
- the implementation target and revision;
- the implementation checkpoint;
- the currently deployed behavior when it differs materially;
- the owner of the pending work; and
- the latest evidence or the fact that no evidence exists yet.

Accepted intent states what the product requires. It does not claim that every
current implementation already conforms.

### 8.5 Overlapping changes and stale review

When two active changes touch the same intent ID or normative term, their owners
MUST choose and record an acceptance order. The change reviewed second MUST use a
proposed revision that includes the first change or explicitly state why the
changes do not interact.

After a proposed intent revision changes, prior acceptance applies only to the
unchanged IDs and wording that the approval record names. Any unaccepted material
edit sets the change checkpoint to `Partially accepted` or `Review required`.

### 8.6 Roles and independent review

One person or agent MAY perform several responsibilities. Projects SHOULD use a
reviewer who did not choose the implementation for high-risk money, safety,
permission, privacy, or irreversible-data changes.

A conformance reviewer SHOULD read accepted intent and evidence before reading
the technical plan. A reviewer who follows this order can seek product
counterexamples without inheriting the implementer’s design assumptions.

## 9. Change classes

### 9.1 Baseline acceptance

A project uses one baseline change when it first accepts product intent. Product
authority MUST review that intent as desired behavior rather than infer it from
current code. The baseline change lists known implementation gaps and gives each
implementation target an honest checkpoint.

### 9.2 Intent change

New, changed, or retired product behavior requires a change record and product
review. Authors edit canonical intent and the change record in the same working
branch when practical.

### 9.3 Clarification

A wording edit that preserves meaning MAY use the repository’s normal review
path without a change record. If reviewers disagree about the old meaning, the
edit changes intent and needs a change record.

### 9.4 Conformance fix

When accepted intent already states the correct behavior, a code fix MUST link
the affected requirement IDs and MUST provide evidence for the defect and likely
regressions.

No conformance fix exists without a requirement. If no accepted requirement
covers the expected behavior, the team first proposes the missing intent.

A project MAY require a change record for high-risk or broad conformance fixes.

### 9.5 Internal change

A refactor or dependency change that cannot alter observable behavior need not
create product intent. The implementer MUST preserve applicable requirements and
SHOULD record risk-based evidence in the project’s normal review system.

If the work changes errors, latency, permissions, retention, compatibility, or
another product boundary, the team treats it as an intent change.

### 9.6 Exploration

A team MAY build a prototype while intent remains draft. The branch and change
record MUST identify the work as exploration. Reviewers MUST NOT treat the
prototype’s behavior as accepted intent or conformant implementation.

### 9.7 Emergency change

A project MAY let an urgent safety, security, or availability fix change code
before intent review. The change MUST name the emergency, limit its scope, and
record known behavior and evidence.

Maintainers MUST name an owner and deadline for intent review and evidence after
immediate harm passes. Maintainers do not gain product authority for a permanent
policy choice by calling a fix urgent.

## 10. Review

### 10.1 Intent review

An intent reviewer MUST check:

- each material choice has a product authority with matching scope;
- each actor can be identified in the real product;
- permissions say who may act and what unauthorized actors observe;
- state rules cover creation, transition, expiry, cancellation, and recovery;
- failures name visible results and ownership of retries;
- concurrent actions preserve every invariant;
- privacy, security, accessibility, and safety rules are explicit when relevant;
- quality claims use conditions and measurable thresholds;
- assumptions do not hide product duties;
- unspecified choices are observable variations that product authority accepts;
- internal mechanics remain absent unless an external boundary requires them;
- each permission, state transition, and flow summary links to the normative IDs
  that govern it; and
- each acceptance method could distinguish conforming from nonconforming
  behavior.

### 10.2 Conformance review

A conformance reviewer MUST:

- name the implementation target;
- read the named accepted intent revision;
- map each affected invariant, requirement, normative scenario, and strong
  default to evidence;
- seek negative, permission, failure, recovery, duplicate, race, time, and
  quality counterexamples where relevant;
- record failed, missing, and inconclusive checks;
- state what each check cannot prove; and
- name the exact implementation revision and environment.

The reviewer MUST check whether any evidence became stale before issuing a
conclusion.

Code review alone does not satisfy this checkpoint.

## 11. Responsibilities

OpenIntent defines responsibilities, not a required cast of personas:

- The **intent author** turns a need or implementation discovery into proposed
  product contract edits and open questions.
- The **intent reviewer** challenges those edits and protects the product
  boundary.
- The **product authority** accepts or rejects product choices within a named
  scope.
- The **implementer** chooses internal mechanics, builds against current intent,
  and MAY propose or edit intent on a working branch when work reveals a gap.
- The **conformance reviewer** tests one implementation target and revision
  against one accepted intent revision and records limits.
- The **discoverer** studies an existing system and keeps observed, intended,
  unknown, and conflicting claims separate.
- The **curator** keeps links, terms, IDs, context routes, and artifact sizes
  coherent without changing product meaning.

A project MAY assign these responsibilities to people, agents, or both. An agent
MUST NOT claim product authority unless repository rules grant that authority
for the exact choice.

## 12. Context control

### 12.1 Context budgets

Projects SHOULD keep common read paths small enough for a new person or agent to
understand without loading the whole repository.

These numbers provide guidance, not conformance gates:

- `intent/product.md`: about 150 lines;
- one glossary entry: one short paragraph;
- one capability file: about 500 lines;
- one change record: about 200 lines; and
- one common implementation task’s intent context: about 2,000 lines.

When common tasks exceed these budgets, curators SHOULD inspect capability
boundaries, repeated text, and unnecessary dependencies.

### 12.2 Splitting capabilities

When one capability outgrows one file, projects SHOULD split it by behavior
topic:

```text
intent/capabilities/
  CAP-DELIVERY/
    index.md
    retries.md
    ordering.md
```

The index keeps the capability metadata, boundary, invariants, and links.
Topic files keep related requirements, scenarios, failure behavior, and
acceptance methods together.

Projects SHOULD NOT split one capability by artifact kind, such as placing all
requirements in one file and all scenarios in another. That split forces every
reader to load several files for one behavior.

Stable IDs MUST survive file moves and splits.

## 13. Repository audits

Projects SHOULD run these audits periodically and after broad contract changes:

1. **Structural audit:** Check required metadata, stable IDs, references, index
   routes, glossary terms, state labels, and open-question owners.
2. **Intent coverage audit:** For each product boundary, find the accepted
   requirement, deliberate `UNSPECIFIED` choice, non-goal, or discovery gap that
   explains it.
3. **Evidence audit:** For each applicable invariant, requirement, normative
   scenario, and strong default, find current evidence for each implementation
   target or a visible missing-evidence marker.
4. **Observed-behavior audit:** Enumerate actor-visible interfaces, events,
   errors, and states in an implementation. Record any behavior that accepted
   intent does not cover.
5. **Context audit:** Find oversized files, stale links, repeated requirements,
   unrelated context routes, and active changes with no owner.
6. **Overlap audit:** Find active changes that touch the same intent IDs or
   normative terms without a recorded acceptance order.
7. **Freshness audit:** Find `Conformant` targets whose intent revision,
   implementation revision, dependencies, or checked conditions have changed.

An observed behavior gap does not automatically become intent. Product
authority chooses whether to capture, change, leave open, or remove it.

A project MAY ask a new implementer to rebuild a bounded capability from intent
and technical constraints, then compare actor-visible behavior. This exercise
tests whether intent supports replacement; OpenIntent does not require routine
regeneration.

## 14. Existing-system adoption

A project with existing code SHOULD adopt OpenIntent incrementally:

1. Add `AGENTS.md`, an intent index, a product file, an authority registry, and
   at least one implementation target.
2. List product areas that accepted intent does not yet cover.
3. Study one bounded area in `discovery/`.
4. Label each source-backed claim `OBSERVED`, `INTENDED`, `UNKNOWN`, or
   `CONFLICT`.
5. Ask product authority which behavior to accept, change, leave unspecified,
   or remove.
6. Add accepted requirements through a baseline or later change record.
7. Repeat where current work makes missing intent costly.

Agents MAY draft observations and proposed intent. Only product authority MAY
turn observed behavior into accepted product intent.

Projects MUST NOT bulk-generate specifications from code and accept them without
human product review. That practice gives accidents and defects the force of
intent.

## 15. Conformance

A repository conforms to OpenIntent 0.1 when it:

1. meets each `MUST` and `MUST NOT` rule in this document;
2. records each deliberate departure from a `SHOULD` or `SHOULD NOT` rule;
3. requires no vendor service, agent, CLI, parser, or schema to read and follow
   its product contract;
4. lets a new reviewer trace an accepted requirement through changes and current
   evidence using repository files and Git; and
5. shows implementation checkpoints and known gaps instead of implying that
   accepted intent already shipped.

An implementation target and revision conform only to a named intent revision.
Their evidence record MUST name the target and revision, cover every applicable
invariant, requirement, and normative scenario, and record how it handled every
applicable `SHOULD` and `SHOULD NOT`.

A change-scoped evidence record may conclude `Conforms` for only the rules in
its stated scope. A project claims that the target conforms to the whole named
intent revision only when current evidence covers every accepted rule that the
intent index applies to that target.

A repository MAY conform while one or more implementation targets remain
pending, unknown, or nonconformant, provided the intent index and change records
state that fact clearly. The repository MUST NOT collapse several targets into
one checkpoint when their revisions or conformance results differ.

Projects SHOULD report the OpenIntent version they follow in `intent/index.md`.
They MUST NOT claim conformance without naming a version.

## 16. Tool and vendor independence

OpenIntent requires no executable tool and defines no machine-readable schema.
Predictable headings, Markdown tables, IDs, and links allow future tools to help
without owning the method.

A future tool MAY validate structure, assemble context, follow links, or compare
evidence. A conforming project MUST remain understandable and operable when that
tool is absent.

No normative rule may require or prefer one coding agent, model vendor, IDE,
programming language, framework, storage system, or hosted service. A conforming
project MUST NOT impose such a requirement through OpenIntent artifacts.
