# Design principles

This guide explains why OpenIntent 0.1 uses its particular rules. The
[standard](../SPECIFICATION.md) remains authoritative.

## 1. Keep product intent above implementation evidence

A source tree can answer many questions about one build. It cannot tell a
reader whether a behavior was deliberate, accidental, temporary, or no longer
wanted. Tests usually preserve behavior selected by earlier developers, but a
passing test does not prove that users still need that behavior.

OpenIntent gives accepted intent files one narrow job: state what the product
should do. Code, tests, telemetry, tickets, and prior releases provide evidence.
People compare that evidence with the product contract instead of quietly
turning it into the contract.

This rule does not make intent infallible. Implementation, tests, users, and
operators can expose a bad or missing requirement. An author updates the
proposed intent, product authority reviews material choices, and the team
continues the implementation loop.

## 2. Specify the boundary and delegate the interior

An intent file should constrain what actors can observe and what the product
must preserve. Implementers should choose modules, frameworks, algorithms,
storage systems, deployment shapes, and internal message paths.

For example:

- Product intent may require that two simultaneous pickup attempts cannot both
  claim one parcel.
- An implementation plan may choose a database constraint, compare-and-swap,
  lock, queue, or single writer.

The first statement survives a complete rewrite. The second helps one
implementation and may disappear with it.

Some technical details sit at a real product boundary. A public protocol, legal
retention format, cryptographic interoperability rule, or hardware interface may
need exact bytes or algorithms. Writers include those details and state which
outside actor requires them.

## 3. Let Git show the delta

OpenIntent writers edit the accepted contract on a branch and review its Git
diff. A nearby change record explains why those edits belong together. The
method does not require writers to maintain a second delta document and later
merge it into the contract.

This choice removes three common failure paths:

- the delta and proposed full text disagree;
- an archive step loses or misapplies a change; or
- an agent loads both copies and treats each as current.

The change record remains valuable because a raw diff cannot explain purpose,
non-goals, rollout risk, or who accepted a product choice.

## 4. Use progressive detail

Every capability does not need the same depth. A writer adds detail where an
implementation choice could change safety, money, permissions, recovery,
compatibility, or another meaningful outcome.

One sentence may fully specify a simple read-only label. A concurrent payment
claim may need states, invariants, timelines, failure results, retry ownership,
and negative scenarios.

OpenIntent templates name review facets but do not require empty sections. A
reviewer asks about every relevant facet and records only the answers that
constrain the product.

## 5. Name uncertainty instead of filling it with guesses

OpenIntent separates four cases:

| Claim | What the writer knows | What happens next |
| --- | --- | --- |
| Intended | A person with product authority accepted the behavior | Put it in an accepted intent file |
| Observed | Named evidence showed an implementation behavior | Keep it in a discovery record until someone decides |
| Unknown | Available evidence cannot answer | Name the missing evidence or decision owner |
| Conflicting | Sources support incompatible answers | Keep both sources and ask a product owner to settle them |

`UNSPECIFIED` means something different from unknown. Product authority uses it
to accept several actor-visible outcomes. An implementer may choose among them.
Authors omit unobservable internal mechanics instead of listing each one as
`UNSPECIFIED`. An agent may not treat missing thought as deliberate freedom.

## 6. Give every obligation a stable handle

Readable IDs let a reviewer connect requirements, changes, tests, and evidence
without a requirements database. IDs also let people discuss one obligation
without quoting wording that may later improve.

OpenIntent uses IDs at the requirement and scenario level, not on every
sentence or source line. Per-line tags add noise and encourage writers to trace
text instead of behavior. A change record names affected IDs. An evidence table
names the same IDs and links to concrete checks.

Permission, state, flow, and transition tables remain useful summaries, but they
cannot hide untagged duties. Each consequential row links to the requirements
that govern it. A normative scenario has its own evidence because it can change
a conformance result.

Semantic slugs such as `CAP-PICKUP.retry-unknown-result` remain readable when a
writer inserts or moves nearby requirements. Automated evidence repeats the ID
in a test name or adjacent comment, and Git trailers can connect a commit to the
same handle.

An ID follows one continuing behavioral duty across revised bounds or conditions.
The intent revision identifies the exact version. Writers retire the ID when the
actor or duty changes enough that old and new evidence should not look
interchangeable.

## 7. Load a context packet, not the repository

The root `AGENTS.md` tells an agent where intent lives. `intent/index.md` maps a
request to a small set of files. Each capability lists the related terms,
qualities, and durable decisions it needs.

A normal implementation agent should need:

1. the nearest `AGENTS.md`;
2. the intent index;
3. one active change record;
4. overlapping active changes, when any exist;
5. affected capability files;
6. only the linked qualities, terms, and decisions;
7. the named implementation target; and
8. the implementation files found during code search.

Historical changes and unrelated capabilities stay outside that packet.

## 8. Assign responsibilities without artificial phases

An intent author, intent reviewer, implementer, conformance reviewer, and
discoverer have different duties. They do not need elaborate personas or
separate agents. One participant may edit intent, code, tests, and evidence when
repository scope permits.

The participant does not need a ceremonial role switch when implementation
exposes a product gap. The author updates proposed intent, and product authority
reviews a material product choice. The team pauses only work that would encode
an unresolved choice.

For a high-risk change, a second reviewer helps because an implementer may
unconsciously read the contract as support for choices already made in code.
The standard asks for independent judgment where risk warrants it, not a fixed
virtual team for every patch.

## 9. Keep the method usable without tools

Predictable Markdown headings and IDs can support a future linter or context
builder. No tool should become the only way to understand the contract.

This constraint protects projects from vendor churn and keeps the first version
honest. If people cannot follow a rule through ordinary files and Git review,
automating that rule will not make its meaning clear.

## 10. Scale review with consequence

A copy change and a financial state transition do not deserve identical process
cost. OpenIntent keeps the artifact types stable while teams vary review depth,
reviewer independence, evidence breadth, and rollout controls.

Teams should spend the most care where a wrong interpretation can cause harm,
lose data or money, expose private information, lock out users, or break an
external contract.
