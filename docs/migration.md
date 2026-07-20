# Adopting OpenIntent in an existing project

Do not ask an agent to reverse-engineer the entire codebase into an authoritative
specification. That approach copies accidental behavior, overwhelms reviewers,
and creates a large contract nobody has accepted.

Adopt OpenIntent one product area at a time, usually when someone needs to change
that area.

Teams can repeat or overlap the steps below as current work reveals new facts.
They do not form a separate implementation process.

## The four-claim rule

Every discovery claim uses one state:

- **OBSERVED:** named evidence showed the behavior in a named revision or
  environment.
- **INTENDED:** a person with product authority confirmed the behavior, and the
  accepted contract contains it or has a linked pending change.
- **UNKNOWN:** available evidence cannot answer.
- **CONFLICT:** named sources support incompatible answers.

These states prevent a common migration mistake: treating the current program as
the product owner.

## 1. Add the routing files

Add a concise root `AGENTS.md` and root `intent/index.md`. For one product, add
`intent/product.md` and use the root index as its product index. For several
products, register each product ID, product index, intent root, authority scope,
dependencies, and implementation targets. The root index names one owner for
every shared contract. Each product file may start with only well-supported
purpose, actors, boundaries, and global invariants. Mark draft text as draft.

Map existing technical guidance separately. Coding style, framework choices,
build commands, and module rules can remain in existing developer documents.
`AGENTS.md` should link to them but should not put them into product intent.

Register component and composition targets separately. A running deployment
that assembles several daemons, applications, devices, or external services may
need its own composition target even when every component comes from the same
repository revision.

## 2. Choose a bounded area

Pick an area with one of these triggers:

- a planned behavior change;
- repeated defects caused by unclear product rules;
- high safety, privacy, permission, money, or recovery risk;
- an upcoming rewrite or vendor replacement; or
- conflicting stakeholder beliefs.

Avoid starting with the largest subsystem. A narrow capability gives reviewers
a complete contract they can actually test.

## 3. Gather sources without ranking them as intent

A discoverer may inspect:

- user and operator interviews;
- policies, contracts, and legal rules;
- current and old code;
- tests and fixtures;
- production traces and telemetry;
- support cases and incidents;
- tickets, design notes, and prior decisions; and
- external interface documentation.

For each claim, record the source path or durable link, revision or date,
environment, and confidence. A newer source is not automatically more
authoritative. A running system can still be wrong.

Existing screenshots, diagrams, schemas, fixtures, audio, and design files are
sources during discovery. Product authority decides whether exact content
should become a normative supporting artifact. Existing benchmark environments
and device matrices can become operating profiles only after reviewers decide
that they describe supported conditions rather than one historical run.

## 4. Build a discovery table

```markdown
| Claim | State | Evidence | Question or next step |
| --- | --- | --- | --- |
| The service retries a controller timeout twice | OBSERVED | `controller_client` at revision `abc123`; trace `T-91` | Ask whether two retries are policy or an old default |
| A recipient may retry without rescanning | CONFLICT | UI copy says yes; API rejects the token after any timeout | Product owner must choose the desired recovery path |
| Operators may force-open a compartment | UNKNOWN | Role map has no entry; one incident mentions a manual open | Interview operations and security owners |
| One parcel may have only one active claim | INTENDED | Safety owner accepted `CAP-PICKUP.one-active-claim`; pending change linked | Add concurrent evidence before acceptance |
```

Do not soften a conflict into vague prose. Keep both incompatible claims visible
until a person chooses.

## 5. Ask product questions

Group questions by consequence, not source file. Ask concrete alternatives:

> When the controller response is lost after a valid pickup claim, should the
> claim remain reserved for the same recipient, return immediately to available,
> or require an operator? Which harm does the product avoid with that choice?

Avoid asking, "Should we preserve current behavior?" That framing gives the
implementation undeserved authority.

Product owners may accept observed behavior, reject it, or deliberately leave a
safe choice unspecified.

## 6. Write the first accepted capability

Turn accepted answers into a capability file through one baseline change.
Include only claims that product authority accepted. Leave unknown and
conflicting claims in discovery until they are settled. If an unknown blocks
predictable conformance, keep the capability draft.

Link every accepted rule back to its migration change record. The record should
name compatibility effects when desired behavior differs from current behavior.

Implementers may find another product need after this review. Update the
proposed intent and change record, ask product authority to review the material
edit, and continue work that does not depend on the answer.

## 7. Measure the conformance gap

Compare each implementation target with the accepted capability:

| Target | Intent ID | Current evidence | Gap | Planned action |
| --- | --- | --- | --- | --- |
| `IMPL-PICKUP-SERVICE` | `CAP-PICKUP.one-active-claim` | Sequential tests only | Concurrent behavior unknown | Add race test before changing claim code |
| `IMPL-PICKUP-SERVICE` | `CAP-PICKUP.retry-unknown-result` | Two retries with new IDs | Violates same-ID retry rule | Change client and verify controller support |
| `IMPL-PICKUP-SERVICE` | `CAP-PICKUP.unavailable-token-disclosure` | API reveals expired parcel ID | Violates disclosure rule | Change error response and review client compatibility |

Do not claim that the project conforms while gaps remain. The project can still
conform to the OpenIntent method because it records those gaps honestly.

## 8. Reconcile safely

Treat each gap as a normal change. Plan data migration, compatibility windows,
rollout flags, user communication, and rollback where needed. Preserve current
behavior only when the accepted contract or a temporary compatibility rule says
to preserve it.

The team may revise intent and implementation several times while it closes a
gap. The change record keeps both checkpoints visible.

When a legacy behavior has unknown consumers, gather evidence before removal.
Unknown consumers create a migration risk, not a permanent product requirement.

## 9. Expand only when useful

Add the next capability when work or risk reaches it. Update the root product map
as accepted areas grow. This incremental path keeps each artifact reviewed and
keeps agent context small.

## Common migration failures

### The generated encyclopedia

An agent writes hundreds of pages from code, and maintainers merge them without
product review. Readers cannot tell accidental behavior from intended behavior.

Fix: keep generated text in `discovery/`, choose one bounded capability, and ask
product owners concrete questions.

### Tests become the contract

Writers copy all test assertions into requirements. Old bugs and technical
details become permanent.

Fix: use tests as evidence. Ask what user, operator, safety, legal, or interface
need each assertion protects.

### Unknown becomes unspecified

Writers label every gap `UNSPECIFIED`, so implementers can choose consequential
behavior.

Fix: use `UNKNOWN` during discovery. Product authority alone can decide that a
choice is safely unspecified.

### The contract never catches up

Teams keep discovery files but continue changing code directly.

Fix: require a change record and product checkpoint for the next observable
change in each adopted area. OpenIntent grows through actual work rather than a
separate documentation campaign.
