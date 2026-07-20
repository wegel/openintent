# Review and evidence

OpenIntent asks three different questions. A reviewer should not answer one and
claim all three.

1. **Does the file follow the standard?** Check structure and links.
2. **Does the contract say the right thing clearly?** Review product meaning.
3. **Does this implementation target and revision meet that contract?** Inspect
   concrete evidence.

## Structural review

The reviewer checks that:

- every Draft, Accepted, and Retired artifact appears in its product index;
- the root index registers products, owned shared contracts, dependencies, and
  cross-product changes;
- each product index registers authority scopes, component and composition
  targets, operating profiles, and normative supporting artifacts;
- every normative rule and scenario has a stable, unique ID;
- every normative permission and transition summary links to governing IDs;
- every linked file and heading exists;
- every scenario names a parent requirement;
- every normative scenario appears in an acceptance map;
- every change names affected IDs and edits their canonical files;
- every accepted change names an authorized approver, proposed revision, IDs,
  result, and date;
- overlapping changes name an acceptance order;
- every evidence record names its target kind, intent revision, implementation
  revision, profiles, and environment;
- every composition record names all participant revisions; and
- intent state, change state, intent checkpoint, and target checkpoints are
  visible.

A future linter could automate many of these checks. A person can perform them
with a text editor and repository search today.

## Semantic review

The reviewer reads as a skeptical product user, operator, attacker, and
replacement implementer.

### Boundary questions

- Can a reader identify every actor and external system?
- Does the capability own the promised result, or does an assumption hide part
  of it?
- Do non-goals exclude plausible scope that an agent might otherwise add?
- Does the contract state externally required technology details and delegate
  internal choices?
- Which product owns each shared contract, and what does each consumer do when
  that contract changes or fails?
- Does a large capability route one behavior topic without forcing unrelated
  context?

### Behavior questions

- What does the first valid action do?
- What do duplicate, stale, malformed, late, and unauthorized actions do?
- Which states exist, and which transitions are illegal?
- What survives a crash between each pair of visible effects?
- What happens when two valid actions race?
- What happens when an outside system returns success late or never returns?
- Who retries, with which identity, how often, and until what terminal result?

### Harm questions

- Can one actor learn that another actor's object exists?
- Can permissions change while work is in flight?
- Can a retry charge money, send a message, open hardware, or mutate data twice?
- Can an operator recover without leaving an audit trail?
- Can a valid action violate accessibility, retention, safety, or legal rules?

### Replaceability questions

- Could two independent implementers understand the same observable result?
- Does any requirement merely restate the current code structure?
- Does `UNSPECIFIED` grant safe actor-visible freedom, or does it hide a missing
  product choice?
- Did the author omit internal mechanics instead of cataloging them as
  `UNSPECIFIED`?
- Could a different implementation produce valid evidence without copying the
  current architecture?
- Does each operating profile define only reusable conditions?
- Does each normative supporting artifact govern exact properties without
  hiding semantic behavior or requiring a hosted editor?

## Adversarial review without forced findings

A reviewer should actively seek counterexamples and missing cases. An agent can
be prompted to assume flaws exist and report them with severity and evidence.

Do not require an agent to invent a finding before approval. A forced quota can
turn harmless preferences into fake defects. The reviewer may return no blocking
findings after describing which boundaries and counterexamples it checked.

People filter agent findings. Agents can misread product context or report a
plausible concern with no support.

## Evidence types

Different claims need different checks.

| Claim | Useful evidence | Common overclaim |
| --- | --- | --- |
| Deterministic rule | Unit or property test | Claiming a mocked dependency proves real integration |
| State transition | Integration test plus final state inspection | Checking only the response and not durable state |
| Concurrent invariant | Controlled race, stress test, or model check | Running sequential requests and calling them concurrent |
| Retry and recovery | Fault injection with attempt and state records | Testing one immediate error without an unknown result |
| Permission boundary | Positive and negative authorization tests | Checking the user interface while leaving the API open |
| Latency or capacity | Timed run under a declared workload and environment | Reporting a local average as a production percentile |
| Accessibility | Automated checks plus assistive-technology review where needed | Treating one scanner as complete accessibility proof |
| Operator workflow | Rehearsal or observed run with an audit record | Reviewing a runbook without trying the steps |
| External compatibility | Contract tests against supported versions | Testing one current version and claiming all supported versions |
| Visual or spatial contract | Rendered comparison plus interaction and accessibility checks | Treating one screenshot as proof for every viewport, state, language, or input mode |
| Audio or temporal contract | Recorded output, timing trace, and human listening where perception matters | Letting clean counters replace an audible or perceptual check |
| Protocol or schema reference | Fixture replay, negative vectors, and cross-implementation exchange | Proving that one parser accepts its own output and calling that interoperability |
| Supported composition | End-to-end check with every participant revision recorded | Combining passing component reports without running the assembly |

One item may need several forms of evidence. The evidence record names limits so
a later reviewer can decide whether risk calls for more.

Each automated check used for conformance includes the most specific intent ID
in its name or an adjacent comment. A check for a normative scenario uses the
scenario ID. That tag lets a reader search from intent to the check without
maintaining a second trace database.

## Coverage table

Use one row per rule by default. Group IDs only when the same check, conditions,
result, and limits apply to every ID:

| Intent ID | Reference | Check | Profile and actual environment | Result | Evidence | Limits |
| --- | --- | --- | --- | --- | --- | --- |
| `CAP-PICKUP.one-active-claim` | none | Race two valid claims 1,000 times and inspect winners | Integration build, two workers | PASS | `tests/...`, run 1842 | Did not simulate process loss after claim write |
| `CAP-PICKUP.retry-unknown-result` | `REF-CONTROLLER-OPEN-V7` | Drop two controller responses and inspect request IDs | Controller simulator 3.2 | PASS | report link | Simulator does not model controller reboot |
| `QLT-RECOVERY.outage-result-time` | none | Five-minute outage at declared traffic | `PROF-PEAK-SITE`; staging | NOT RUN | issue link | Staging controller unavailable |

A missing check remains a visible row. When no applicable rule has failed, that
gap forces `Not determined`. Release owners may accept operational risk, but
they cannot turn missing evidence into conformance.

## Interpreting normative words

### MUST and MUST NOT

Every applicable invariant, requirement, and normative scenario needs passing
evidence for target conformance. If a reviewer cannot check the rule, the record
says `NOT RUN` or `INCONCLUSIVE` and the target cannot claim conformance.

### SHOULD and SHOULD NOT

The normal path should have evidence. A departure must state:

- the exceptional condition;
- why the normal rule would cause greater harm or cannot apply;
- the chosen behavior;
- consequences; and
- who accepted the departure.

A team should change an inaccurate SHOULD rule instead of collecting permanent
exceptions around it.

### MAY

The evidence record should identify which permitted choice the implementation
makes, and the reviewer should check that other requirements still hold. A MAY
rule does not permit behavior that a MUST NOT rule forbids.

### UNSPECIFIED

No conformance test should require one unspecified choice. Reviewers may still
test that the actor-visible choice cannot escape its stated boundary.

## Evidence freshness

An evidence record applies to one target, one intent revision, one
implementation revision, named profile revisions, an environment, and a set of
conditions. A composition record also applies to its exact participant
revisions. Later intent, code, participant, profile, supporting-artifact,
dependency, configuration, data shape, or infrastructure changes can make it
stale.

Projects should rerun evidence when:

- code touches an affected requirement path;
- a dependency changes behavior at the boundary;
- a composition participant revision changes;
- an applicable operating profile or normative supporting artifact changes;
- operating conditions move outside the measured range;
- an incident contradicts the prior result; or
- a reviewer changes the requirement.

When evidence becomes stale, the target returns to `Unknown` until a reviewer
checks current evidence. The index links the latest accepted evidence per target;
it does not become a dashboard for every test run.

## Acceptance decision

The evidence record ends with one of these conclusions:

- **Conforms:** every applicable invariant, requirement, and normative scenario
  passed, except that a strong default may have an accepted departure.
- **Does not conform:** evidence contradicts at least one applicable invariant,
  requirement, or normative scenario, even if other rules remain untested.
- **Not determined:** no applicable rule failed, but missing, stale, not-run, or
  inconclusive evidence prevents a conformance claim.

Every conclusion records its limits. A limit narrows the claim but cannot hide a
required condition that the evidence did not establish. The reviewer signs the
conclusion and date. A release owner may accept operational risk, but that choice
cannot turn failed or missing evidence into conformance.

The record states whether it checks one change's rules or every accepted rule
that applies to the target. A passing change-scoped record does not prove whole-
target conformance. The intent index may show `Conformant` only when the current
evidence set covers the whole target scope.

A component and a composition keep separate conclusions. A component result
does not prove that a supported assembly interoperates. A composition result
does not prove that one component works in another assembly or outside the
checked profile.

## Future formal checks

Stable IDs, state tables, scenario syntax, and evidence maps can later feed
linters, property tests, model checkers, or formal models. Projects should add
those checks where their risk justifies them.

OpenIntent does not require formal proof. A tool-generated proof or report still
links to a human-readable requirement and states its assumptions.
