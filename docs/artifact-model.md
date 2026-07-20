# Artifact model

OpenIntent uses a small set of files with distinct jobs. When one file tries to
serve two jobs, implementation detail tends to leak into product intent or old
history tends to look current.

## Relationship map

```text
                     repository index and ownership
                    +--------------------------------+
                    | products -> owned contracts    |
                    |          -> target relations   |
                    |          -> dependencies       |
                    +--------------------------------+
                                   |
                          product contract
                    +--------------------------------+
                    | product -> capabilities        |
                    |         -> qualities           |
                    |         -> profiles            |
                    |         -> glossary            |
                    | rules   -> supporting artifacts|
                    +--------------------------------+
                           ^                 |
                           | proposed edits  | guides
                           |                 v
need -> change/change.md <------> named implementation targets and tests
              |                         |
              | technical choices       | concrete results
              v                         v
          plan.md (optional) <------ evidence.md

discovery/*.md supplies observations and questions to a proposed change.
It never points directly into accepted intent without product review.
```

The product contract answers "what should the product do?" Change and decision
records answer "why did people choose this?" Plans answer "how will this
implementation work?" Evidence answers "what did reviewers actually check?"
Implementers may expose a product gap as they build and test, then send proposed
intent back through review.

## Artifact catalog

| Artifact | Default path | Authority | Main reader | Job |
| --- | --- | --- | --- | --- |
| Agent guide | `AGENTS.md` | Repository rules | Every agent | Route the reader and define safe behavior |
| Repository index | root `intent/index.md` | Accepted ownership and routing map | Every multi-product task | Route products, shared contracts, dependencies, compositions, and cross-product work |
| Product index | `<intent-root>/index.md` | Accepted contract and target map | Every product task | Route context, authority, active work, targets, profiles, references, and gaps |
| Product | `<intent-root>/product.md` | Accepted intent | Product owner, any agent | Define purpose, boundary, actors, global invariants, and capability map |
| Glossary | `<intent-root>/glossary.md` | Accepted terminology | Anyone reading intent | Give ambiguous domain words one product meaning |
| Capability | `<intent-root>/capabilities/CAP-*.md` or `CAP-*/index.md` | Accepted intent | Author, implementer, reviewer | Define one coherent product ability in one file or behavior-topic directory |
| Quality | `<intent-root>/qualities/QLT-*.md` | Accepted intent | Author, implementer, reviewer | Define measurable rules that span capabilities |
| Operating profile | `<intent-root>/profiles/PROF-*.md` | Accepted conditions | Author, implementer, reviewer | Define reusable workload, data, device, platform, topology, or failure conditions without creating a duty |
| Normative supporting artifact | `<intent-root>/references/REF-*.md` plus checked-in source | Accepted intent within governing rule scope | Author, designer, protocol author, reviewer | Carry exact visual, audible, protocol, schema, fixture, diagram, or other detail in the medium that communicates it best |
| Durable decision | `<intent-root>/decisions/DEC-*.md` | Explanatory | Future author | Preserve why maintainers chose a long-lived product policy |
| Change | `changes/CHG-*/change.md` | Explanatory; current state is explicit | Product owner, reviewers | Explain one coherent contract edit and its risk |
| Plan | `changes/CHG-*/plan.md` | Implementation aid | Implementer | Map accepted outcomes to technical work |
| Evidence | `changes/CHG-*/evidence.md` | Review record | Conformance reviewer | Map affected rules to checks and results |
| Discovery | `discovery/*.md` | Evidence staging | Discoverer, product owner | Separate observed, intended, unknown, and conflicting claims |
| Implementation target | Intent index or `implementations/IMPL-*.md` | Implementation inventory | Implementer, reviewer | Keep one component or composition target's owner, revision, relationships, intent revision, checkpoint, and evidence distinct |

Permission, state, flow, and transition tables summarize named normative rules.
They do not create untagged duties. Each consequential row links to the IDs that
govern it.

## Product ownership and dependencies

A repository index routes products; it does not become an umbrella product
contract. Each shared protocol, user journey, data boundary, or operator
contract has one owning product and one canonical set of intent IDs. Consuming
products link to those IDs and state what they do when the dependency changes or
fails.

A cross-product change may edit several owned contracts. The change records one
coordinator and separate approvals from each affected authority scope. One
owner's approval cannot accept another product's rules.

## Conditions, supporting artifacts, and evidence

An operating profile answers "under which supported conditions?" A capability
or quality rule answers "what must happen?" An evidence record answers "what
did this exact revision do under the actual conditions?" Keeping those answers
separate lets several requirements reuse a large-device, low-memory, peak-load,
or degraded-network definition without turning one benchmark run into policy.

A normative supporting artifact carries exact detail that prose communicates
poorly. Its Markdown record names the governed properties, allowed variation,
and parent requirements. The parent text still names the actor, state, result,
and reason the exact detail matters. A screenshot captured from a build remains
evidence; it becomes product intent only when an accepted reference record and
governing requirement say so.

## Component and composition targets

A component target can pass its own contract and still fail when paired with a
specific peer, device, daemon, or protocol revision. A composition target names
the supported assembly and records the exact participant revisions. Reviewers
check the assembly separately. They do not copy component conclusions into the
composition or use one successful assembly to certify a component everywhere.

## Why scenarios stay with capabilities

A separate scenario catalog can make one user journey easy to browse, but it
also creates a second behavior source. Writers then need to decide whether a
requirement or a scenario wins.

OpenIntent nests normative scenarios under the requirement they explain. A
capability may link scenarios across requirements when a long workflow needs a
reader-friendly overview, but that overview remains non-normative. The nested
scenarios keep each context packet self-contained.

## Why examples stay non-normative

Examples help readers understand a rule, especially at a boundary. They rarely
cover the full valid space. If an example silently sets a rule, another valid
case may appear invalid.

Writers mark examples as `EXAMPLE` and express every obligation with a
requirement. A concrete forbidden case needs a `MUST NOT` parent requirement.

## Why questions stay near active work

A global question backlog grows quickly and forces agents to read unrelated
uncertainty. OpenIntent keeps an open question in the change or discovery record
that exposed it. The affected intent cannot become accepted while the question
blocks predictable conformance.

A project may use an issue tracker to assign questions. The local record still
keeps the question, owner, and durable link so a future reader does not depend
on search or chat history.

## Why evidence stays separate from intent

Authors should write intent that survives implementation replacement. Test
paths, build revisions, environments, and screenshots belong to one
implementation and become stale at a different rate.

An acceptance map in each capability describes the kind of evidence a reviewer
needs. A change evidence record points to the actual evidence for one revision.
This split keeps the contract stable while checks evolve.

Product files keep an acceptance map for product-wide invariants. Normative
scenarios also appear in acceptance maps because they can change a conformance
result.

## Why plans remain optional

An implementer may need a durable plan for a broad or risky change. A small fix
may need only the affected requirement IDs and a test. Requiring a design and
task file for every change rewards paperwork rather than clear product intent.

When a plan exists, it may name architecture, modules, data storage, libraries,
algorithms, rollout steps, and tasks. None of those choices becomes product
intent merely because the plan records it.

## States and checkpoints

Accepted intent artifacts use these states:

| Status | Meaning |
| --- | --- |
| Draft | Reviewers may discuss the file, but implementers cannot treat it as a product rule |
| Accepted | The file forms part of the contract on the accepted branch |
| Retired | The file serves as a tombstone and points to its replacement or removing change |

Git branches carry proposals. An accepted file edited on a branch remains a
proposal until maintainers merge it to the accepted branch.

Change records track three independent fields:

| Field | Allowed values |
| --- | --- |
| Change state | Active, Completed, Withdrawn |
| Intent checkpoint | Draft, Partially accepted, Accepted, Review required |
| Implementation checkpoint | Not started, Exploring, In progress, Evidence ready, Conformant, Nonconformant, Unknown, Not applicable |

Projects may add states, but `AGENTS.md` must explain them. A state label never
substitutes for the named reviewer and date in the change record.

The intent checkpoint applies to one proposed revision. An accepted artifact
edited on a branch remains an accepted lifecycle artifact, but its edits remain
proposals. When a test exposes a product gap, the author edits proposed intent
and sets the change checkpoint to `Review required`. Product authority reviews
the material edit, and the loop continues.

Each implementation checkpoint belongs to one target, implementation revision,
and intent revision. When any of those inputs or checked conditions change, the
project marks stale evidence and returns the target to `Unknown` until review.

The checkpoint also has a rule scope. A target row in one change covers that
change's affected and preserved IDs. The target row in the intent index covers
every accepted rule that the index applies to that target. Maintainers may mark
the index row `Conformant` only when one or more current evidence records cover
that full set.

## Context packets

The product index should list a context packet for each capability. For example:

| ID | Path | Read with | Triggers |
| --- | --- | --- | --- |
| `CAP-PICKUP` | `intent/capabilities/CAP-PICKUP.md` | `intent/glossary.md#claim`, `QLT-RECOVERY`, `PROF-PEAK-SITE`, `REF-CONTROLLER-OPEN-V7` | pickup, token, claim, compartment door |

An agent starts with the row that matches the request. It follows explicit links
when a requirement needs more context. It does not read every historical change
or decision "just in case."

For a modular capability, its `index.md` provides a second routing step. The
agent reads only the behavior topic and the profiles or supporting artifacts
that topic names.

## Artifact precedence in practice

Suppose a test allows five retries, an old decision says three, a change summary
says "limited retries," and `CAP-NOTIFY.attempt-limit` says the service must make exactly
four attempts. The accepted capability requirement controls product intent.
The reviewer reports that the test and old decision disagree, then checks whether
the implementation makes four attempts.

If two accepted requirements give different answers, no precedence trick fixes
the product contract. An agent reports the conflict and asks a person with
product authority to amend the contract.
