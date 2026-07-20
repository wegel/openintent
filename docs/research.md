# Prior work and design choices

This review uses public material available on 2026-07-18. It explains which
ideas OpenIntent 0.1 borrowed, changed, or rejected. Product names and features
may change after that date.

## Comparison

### OpenSpec

[OpenSpec](https://github.com/Fission-AI/OpenSpec) separates current specs from
change folders and emphasizes brownfield changes. Its change folders collect a
proposal, specification deltas, a design, and tasks. Its archive step applies
`ADDED`, `MODIFIED`, and `REMOVED` sections to canonical specs. It supports many
coding agents through generated commands and an `AGENTS.md` handoff.

What OpenIntent keeps:

- current intent has a stable home;
- one folder groups the purpose and work for a change;
- reviewers see explicit behavioral deltas before or during implementation; and
- agent choice should not own the specification.

What OpenIntent changes:

- Writers edit canonical intent on a Git branch because Git already shows the
  exact delta. A second delta copy and archive merge add drift risk when the
  method has no tool.
- Change records exclude technical approach from normative intent.
- Projects need no Node.js CLI, generated slash command, configuration file, or
  archive operation.
- Canonical files state intended behavior. Evidence separately says whether the
  current implementation matches it.

### GitHub Spec Kit

[GitHub Spec Kit](https://github.github.io/spec-kit/) uses a staged
specification, plan, tasks, and implementation flow. Its current command set
also offers clarification, checklists, cross-artifact analysis, extensions,
presets, workflows, and agent integrations. A project constitution holds
cross-project rules.

What OpenIntent keeps:

- intent review should precede technical planning;
- clarification and adversarial analysis deserve explicit checkpoints;
- reusable templates improve consistency; and
- project-wide principles need a durable repository home.

What OpenIntent changes:

- `AGENTS.md` routes agent behavior, while `intent/product.md` and quality files
  hold product-wide rules. One constitution should not mix coding conventions,
  product policy, and method rules.
- A plan and task artifact remains optional because small changes may not need
  both.
- The standard has no initializer, script layer, command catalog, extension
  registry, or active vendor integration.
- Stable requirement IDs and evidence records provide direct conformance links
  after implementation.

### Kiro Specs

[Kiro Specs](https://kiro.dev/docs/specs/) produces `requirements.md`,
`design.md`, and `tasks.md`, then runs tasks through Kiro's IDE, CLI, or web
surface. Its requirements-first flow uses EARS-style event statements and asks
users to approve phases. It also supports bug and design-first variants.

What OpenIntent keeps:

- observable event and response scenarios make requirements testable;
- people should review requirements before design;
- bug work needs expected behavior and regression boundaries; and
- implementers should verify work as tasks complete.

What OpenIntent changes:

- The repository contract works outside Kiro and has no button or slash-command
  lifecycle.
- Capability files persist after one feature finishes, while change files record
  history.
- `GIVEN`, `WHEN`, and `THEN` are useful forms, not mandatory syntax for every
  rule.
- Architecture and technology choices remain implementation aids rather than
  product authority.

### codemix

[codemix](https://codemix.com/) presents a living product model built from
conversations, specifications, decisions, issues, and code. It calls its
variable level of detail "gradual specification" and uses a hosted knowledge
graph, CLI, agent steering, and semantic review.

What OpenIntent keeps:

- teams should add precision where a choice matters and keep broad strokes
  elsewhere;
- agents need current product meaning rather than scattered historical text;
- semantic review should compare code with intent; and
- existing code should not silently become truth.

What OpenIntent changes:

- Markdown files and explicit links replace a hosted product model.
- Product authority stays reviewable in Git when the service or vendor is
  absent.
- A small intent index routes context without requiring a knowledge graph.
- Human review, not automated model updates, promotes a discovered claim into
  accepted intent.

### BMAD Method

The [BMAD workflow map](https://docs.bmad-method.org/reference/workflow-map/)
uses progressive phases for analysis, planning, technical design, stories, and
implementation, with a smaller quick path for simple work. BMAD also documents
[adversarial review](https://docs.bmad-method.org/explanation/adversarial-review/)
and a project context file for agent implementation rules.

What OpenIntent keeps:

- teams should vary process depth with the work;
- focused story or capability context helps an implementer;
- reviewers should actively search for omissions and counterexamples; and
- technical project rules deserve a stable agent-readable location.

What OpenIntent changes:

- Roles name responsibilities rather than a required team of agent personas.
- Projects do not need phase-specific skills, reports, agent menus, sprint
  artifacts, or a module ecosystem.
- Adversarial reviewers seek counterexamples but do not need to invent a defect
  quota. People filter agent findings.
- Technical project context stays distinct from product intent even when
  `AGENTS.md` links both.

### AGENTS.md

[AGENTS.md](https://agents.md/) offers a simple, open repository entry point for
coding agents. Its scope and nested-file convention make it a strong portability
layer.

OpenIntent makes root `AGENTS.md` canonical for agent routing. It stays concise
and points to accepted intent, active work, implementation guidance, and checks.
Vendor files may provide a handoff but may not fork product rules.

### IETF practice and BCP 14

The [IETF standards process](https://datatracker.ietf.org/doc/rfc2026/) values
clear documents, open review, implementation experience, and evidence before a
specification matures. [BCP 14](https://www.rfc-editor.org/info/bcp14/) gives
`MUST`, `SHOULD`, and `MAY` precise meanings and limits their special meaning to
uppercase use.

OpenIntent borrows the small normative vocabulary, public review record, and
respect for working evidence. A product repository does not need the IETF's
publication bodies, consensus process, or standards-track stages for every
feature.

### Decision records

Michael Nygard's
[architecture decision record](https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions)
keeps context, a decision, and consequences in a short durable file.

OpenIntent uses the same lightweight idea for product choices that future
implementations must understand. It does not let a decision record hide a
behavioral rule. Authors update the affected capability or quality requirement
at the same time. Internal architecture records stay outside accepted intent.

## Prompt ideas examined

The project brief suggested several possible artifacts, words, sections, and
roles. OpenIntent 0.1 changes that draft in these ways.

### Artifact types

| Suggested item | OpenIntent choice | Reason |
| --- | --- | --- |
| Product | Keep | Gives all capabilities one purpose, boundary, actor set, and global invariant list |
| Repository and product indices | Keep routing separate from behavior | Lets a multi-product repository name one owner per contract and load one product's context at a time |
| Glossary | Use when terms are shared or ambiguous; split by domain when large | Stops agents from assigning different meanings without forcing an empty file |
| Capabilities | Keep as the primary behavior unit; split large ones by behavior topic | Gives agents a coherent, bounded context packet without separating requirements from their scenarios and evidence methods |
| Quality requirements | Keep separately when cross-cutting | Prevents repeated or vague quality claims |
| Operating profiles | Keep reusable supported conditions separate from duties | Lets several rules and evidence records name the same workload, platform, topology, or failure condition without copying it |
| Normative supporting artifacts | Keep exact governed content with a Markdown scope record | Lets visual, audio, protocol, schema, fixture, or diagram detail use its clearest medium without hiding semantic rules |
| Decisions | Keep as explanatory records | Preserves reasons without creating a second contract |
| Scenarios | Nest under requirements | Keeps behavior and its boundary examples together |
| Examples | Keep inside relevant artifacts and mark non-normative | Prevents a separate example catalog from becoming hidden authority |
| Changes | Keep one stable folder per coherent change | Connects purpose, Git diff, plan, and evidence |
| Questions | Keep in the active change or discovery record | Avoids a global backlog that every agent must load |
| Evidence | Keep per implementation target and revision within a change | Prevents several builds or release lines from sharing one conformance claim |
| Component and composition targets | Register separately | Prevents a component check from claiming that an assembled system works |

### Capability sections

OpenIntent merges purpose and scope into **Outcome and boundary**. It keeps
actors with permissions because permission rules need named actors. It uses
invariants, requirements, scenarios, and state tables as the behavioral core.
Permission and transition tables summarize named rules rather than creating
untagged duties.

Failure, recovery, concurrency, ordering, time, privacy, security, and
accessibility act as required review facets when relevant. They do not force
empty headings into every capability. A `MUST NOT` requirement replaces an
informal forbidden-scenarios list. Authors omit unobservable internal mechanics.
An optional **Unspecified observable behavior** section names variation that
product authority accepts. An acceptance map describes needed evidence; the
change evidence file records actual results.

### Vocabulary

OpenIntent keeps the five common BCP 14 levels: `MUST`, `MUST NOT`, `SHOULD`,
`SHOULD NOT`, and `MAY`. It rejects `PREFER` because `SHOULD` already expresses a
strong default with accountable exceptions.

`ASSUMPTION`, `UNSPECIFIED`, `OPEN QUESTION`, `NON-GOAL`, `RATIONALE`, and
`EXAMPLE` remain labels rather than requirement levels. The method rejects
`ASSUME` as an instruction and `UNRESOLVED` as permission to guess.

### Roles

The intent author, intent reviewer, implementer, conformance reviewer,
discoverer, and curator remain distinct responsibilities. OpenIntent adds a
product authority because an agent reviewer cannot accept a business tradeoff by
itself. One participant may edit intent and implementation without a ceremonial
role switch. Product authority still accepts material product choices.

### Traceability

OpenIntent uses semantic stable IDs, paths, test tags, Git trailers, and Git
history. It does not require per-line citations, a trace database, or a generated
matrix. A change names affected IDs; an evidence table maps those IDs, one
implementation target, and two named revisions to checks.

### Context size

The intent index and explicit "read with" links replace repository-wide context.
Capabilities own local scenarios and terms. Old changes remain searchable by ID
but stay out of the normal context packet. Suggested file and read-path budgets
help curators detect context that has become too broad.

## Open questions for field use

OpenIntent needs real project evidence before 1.0 can settle these questions:

- How small can the required artifact set become without losing conformance
  clarity for low-risk projects?
- When do teams benefit from separate intent and implementation pull requests?
- Which checkpoint fields best support teams that revise intent repeatedly while
  they implement and test?
- Which metadata fields remain useful enough to standardize across domains?
- How often do stable IDs create merge friction, and which naming schemes work
  best in large monorepos?
- Which evidence links remain durable across test and hosting systems?
- Can teams keep accepted intent current without a linter, and which failures
  justify the first optional tool?

These questions belong to OpenIntent's own evolution. Adopting projects should
not treat them as gaps in their product contracts.
