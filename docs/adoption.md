# Adoption guide

A project can adopt OpenIntent with files and Git. It does not need to install a
program, connect a service, or choose one coding agent.

## New project

### 1. Copy the starter files

Copy these templates into the target repository:

```text
templates/AGENTS.md                 -> AGENTS.md
templates/intent-index.md           -> intent/index.md
templates/product.md                -> intent/product.md
templates/capability.md             -> intent/capabilities/CAP-<NAME>.md
```

When one repository contains several independently owned products, copy
`templates/repository-index.md` to the root `intent/index.md` and give each
product its own intent root and product index. A single-product repository uses
`templates/intent-index.md` at the root as before.

Create empty `intent/qualities/`, `intent/decisions/`, `changes/`, and
`discovery/` directories only when the first file needs them. Git does not need
empty directory placeholders.

### 2. Name product authority

Fill the product authority registry in `intent/index.md`. For each scope, name
who may accept product behavior, who may delegate a narrower choice, who resolves
overlap, and where acceptance appears. The root `AGENTS.md` points to that
registry.

An agent can help elicit, write, challenge, and test intent. Do not make an agent
the implicit product owner simply because it produced the first draft.

### 3. Write the product boundary

Fill `intent/product.md` with purpose, actors, outcomes, non-goals, global
invariants, assumptions, and an initial capability map. Keep unknown details out
or mark the file draft.

### 4. Name implementation targets

Add one index row for each independently checked service, application, device,
supported release line, or supported composition. A small project usually
begins with one target. Do not combine targets whose revisions or conformance
results can differ. A composition row names its component targets and external
participants; it does not inherit their conformance results.

### 5. Start the baseline change and vertical capability

Choose one outcome that crosses the real product boundary. Write enough
requirements and scenarios to implement and accept it. Include failure,
permissions, time, and concurrent behavior only where relevant.

Avoid splitting capabilities by code layer. "Database," "API," and "frontend"
usually describe implementation. "Claim a parcel" or "revoke a team invite"
describes a product ability.

Create one baseline change record before asking for intent review. Set the change
state to `Active` and the intent checkpoint to `Draft`. Give each implementation
target its own row with `Not started`, `Exploring`, `Unknown`, or another honest
checkpoint.

### 6. Review, implement, and revise

Use [the intent review prompt](../prompts/review-intent.md), settle blocking
questions, and record who accepted each material product choice.

Implementers will often find missing or incorrect intent while they build and
test. Update the affected intent on the working branch and the change record,
return material choices to product review, and continue independent work. The
same person or agent may edit intent and code. OpenIntent tracks product
authority and artifact state rather than forcing separate phases.

### 7. Require evidence before conformance

Add one evidence record for each implementation target when that target reaches
`Evidence ready`. Project review rules should reject a `Conformant` checkpoint
that lacks affected requirement IDs or leaves evidence gaps hidden. A project
may accept and merge intent before implementation starts; the target keeps its
honest pending or unknown checkpoint.

Each evidence record names one implementation target, its immutable revision,
and the accepted intent revision. A composition record also names every
participant revision. When accepted intent has no conformant target yet, keep
each target state visible in the intent index instead of inventing evidence.

### 8. Add profiles and supporting artifacts only when they remove ambiguity

Create an operating profile when several rules or evidence runs need the same
workload, data, device, platform, topology, or failure conditions. The profile
defines those conditions once; capability and quality rules still own the
required behavior and threshold.

Create a normative supporting-artifact record when exact visual, audible,
protocol, schema, fixture, diagram, or other checked-in content forms part of
the product boundary. The governing requirement explains why the exact detail
matters, and the record states governed properties and allowed variation. Test
captures and exploratory designs remain evidence or design history.

## Existing project

Follow [the migration guide](migration.md). Start with routing files and one
bounded capability. Keep generated or reverse-engineered claims in `discovery/`
until a person accepts them.

## Minimal project layout

```text
AGENTS.md
intent/
  index.md
  product.md
  capabilities/
    CAP-FIRST.md
changes/
  CHG-YYYYMMDD-FIRST/
    change.md
```

Add glossary, quality, decision, plan, discovery, and detailed implementation
target files when the product needs them. Add profile, reference, or modular
capability files only when their concrete job exists. Add an evidence record
before a target claims conformance. Do not create empty documents to make the
tree look complete.

## Team policy choices

OpenIntent leaves several Git and release choices to each project. Record them
in `AGENTS.md` or linked contributor guidance:

- the accepted branch;
- the product authority scopes, delegation limits, and conflict resolvers;
- whether intent and code share one pull request;
- which risk classes need an independent reviewer;
- how reviewers record approvals;
- which checks run before merge;
- how the project handles accepted future intent;
- how quickly emergency changes must reconcile intent; and
- where technical architecture rules live.

These project rules must not change the meaning of OpenIntent normative words.

## Monorepo adoption

Use the root `AGENTS.md` for repository-wide rules and the root intent index for
product ownership and routing. Give each independently owned product a product
index and registered intent root:

```text
AGENTS.md
intent/index.md
products/
  lockers/
    AGENTS.md
    intent/
      index.md
      product.md
    changes/
  courier-console/
    AGENTS.md
    intent/
      index.md
      product.md
    changes/
```

The root index says which product owns each shared behavior or interface. A
requirement has one owner even when several products consume it. Other products
link to that requirement rather than copying it. The root index also routes
cross-product changes and repository-wide composition targets.

One change may span products. It names one coordinator, lists every affected
product index, routes from the root and each affected product index, and records
each product authority's approval separately.

## Existing documentation

Do not move every document into `intent/`. Classify documents by job:

| Existing content | Suggested home |
| --- | --- |
| Product behavior and invariants | Accepted capability or quality files after review |
| Repeated workload, platform, device, or topology conditions | Operating profile after product review |
| Canonical visual, audio, protocol, fixture, or diagram detail | Normative supporting artifact only when a governing requirement makes the exact content part of the boundary |
| Product rationale | Durable decision or change record |
| Technical architecture | Existing engineering docs or change plan |
| Setup and build commands | `AGENTS.md` or linked developer guide |
| Current behavior found in code | Discovery record until accepted |
| Test output and screenshots | Evidence record links |
| Roadmap ideas | Product planning system, not accepted intent |

## Adoption check

A new coding agent should be able to answer these questions without chat
history:

1. Which branch holds accepted intent?
2. Which files define the affected product behavior?
3. Which choices may an implementer make?
4. Which open questions block work?
5. Which change approved the current rule?
6. Which implementation target and revision does the evidence check?
7. Who can accept a new product choice?
8. Which product owns each shared contract?
9. Does the task check a component or an exact composition?
10. Which profiles and normative supporting artifacts apply?

If the agent must read the entire repository to answer, improve the intent index
and links before adding more specification text.
