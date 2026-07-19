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
or supported release line. A small project usually begins with one target. Do not
combine targets whose revisions or conformance results can differ.

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
and the accepted intent revision. When accepted intent has no conformant target
yet, keep each target state visible in the intent index instead of inventing
evidence.

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
target files when the product needs them. Add an evidence record before a target
claims conformance. Do not create empty documents to make the tree look
complete.

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

Use the root `AGENTS.md` for repository-wide rules and a root intent index for
routing. Give each independently owned product a nested entry point:

```text
AGENTS.md
intent/index.md
products/
  lockers/
    AGENTS.md
    intent/
    changes/
  courier-console/
    AGENTS.md
    intent/
    changes/
```

The root index says which product owns shared behavior. A requirement should
have one owner even when several implementations consume it. Other products
link to that requirement rather than copying it.

## Existing documentation

Do not move every document into `intent/`. Classify documents by job:

| Existing content | Suggested home |
| --- | --- |
| Product behavior and invariants | Accepted capability or quality files after review |
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

If the agent must read the entire repository to answer, improve the intent index
and links before adding more specification text.
