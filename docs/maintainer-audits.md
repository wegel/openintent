# Maintainer audits for OpenIntent itself

This guide gives OpenIntent maintainers one repeatable check for changes to this
repository. It does not add requirements for adopting projects. The normative
rules remain in [SPECIFICATION.md](../SPECIFICATION.md).

Run the relevant audits after any broad contract edit and run every audit before
the first public release. Record each result in the repository review that
accepts the change.

## Audit record

Copy this table into the review record:

| Audit | Result | Files or evidence checked | Remaining problem | Owner |
| --- | --- | --- | --- | --- |
| Normative model | PASS, FAIL, or NOT APPLICABLE | `<paths>` | `<none or concrete problem>` | `<person>` |
| Authority and state | PASS, FAIL, or NOT APPLICABLE | `<paths>` | `<none or concrete problem>` | `<person>` |
| Target and evidence scope | PASS, FAIL, or NOT APPLICABLE | `<paths>` | `<none or concrete problem>` | `<person>` |
| Templates and prompts | PASS, FAIL, or NOT APPLICABLE | `<paths>` | `<none or concrete problem>` | `<person>` |
| Parcel example | PASS, FAIL, or NOT APPLICABLE | `<paths>` | `<none or concrete problem>` | `<person>` |
| Links and IDs | PASS, FAIL, or NOT APPLICABLE | `<paths>` | `<none or concrete problem>` | `<person>` |
| Vendor and tool independence | PASS, FAIL, or NOT APPLICABLE | `<paths>` | `<none or concrete problem>` | `<person>` |

`NOT APPLICABLE` needs a reason. A maintainer does not accept a broad normative
change or publish OpenIntent while a required audit says `FAIL`.

## 1. Normative model

1. List each new or changed `MUST`, `MUST NOT`, `SHOULD`, and `SHOULD NOT` in
   `SPECIFICATION.md`.
2. For each rule, identify the actor, action, conditions, and result in concrete
   words.
3. Check that one term has one meaning throughout the specification.
4. Check that a guide explains any rule that a reasonable adopter could not
   apply from the specification alone.
5. Check that no guide, template, prompt, role card, or example contradicts the
   rule.

## 2. Authority and state

1. Follow a material product choice from an artifact's authority scope to the
   registry and then to a named person's approval.
2. Follow a proposed edit through `Draft`, `Partially accepted`, `Accepted`, or
   `Review required` without treating an unmerged edit as accepted intent.
3. Confirm that `Completed` leaves no required work in that change.
4. Confirm that a decision record explains accepted intent but does not create a
   hidden product rule.
5. Confirm that overlapping changes name their order, rebase point, or resolver.

## 3. Target and evidence scope

1. Select each implementation target independently.
2. Confirm that every checkpoint names a target, implementation revision,
   accepted intent revision, and rule scope.
3. Confirm that a change-scoped `Conforms` result does not become a whole-target
   claim unless current evidence covers every accepted rule for that target.
4. Confirm that a second target cannot borrow another target's revision,
   checkpoint, or evidence.
5. Change one behavior-relevant revision in the review thought experiment and
   confirm that the rules return stale evidence to `Unknown`.
6. Select a composition target, change one participant revision, and confirm
   that component evidence cannot keep the composition conformant.
7. Change an applicable profile or normative supporting artifact and confirm
   that dependent evidence becomes stale.

## 4. Templates, prompts, and roles

1. Start from the minimum files in [adoption.md](adoption.md) and fill every
   required field without inventing a missing concept.
2. Compare each required specification field with the matching template.
3. Follow each prompt as written and confirm that it requests every target,
   authority, overlap, revision, scenario, and evidence field that its task
   needs.
4. Confirm that each role card grants only the authority that the specification
   allows.
5. Confirm that optional files are clearly optional and the minimum file set
   remains usable without them.
6. Build one single-product index and one multi-product root index from the
   templates. Confirm that shared contracts have one owner and every consumer
   can route to it.
7. Build one modular capability from its index and topic templates. Confirm
   that each behavior topic keeps its requirements, scenarios, and acceptance
   methods together.
8. Fill one operating profile and normative supporting-artifact record. Confirm
   that the profile creates no duty and the reference hides no semantic rule.

## 5. Parcel example

Use [the parcel locker example](../examples/parcel-locker/README.md) as an
executable thought experiment:

1. Follow every permission and state-transition summary to governing intent
   IDs.
2. Find every product invariant, requirement, and normative scenario in an
   acceptance map.
3. Find every accepted rule that applies to `IMPL-PICKUP-SERVICE` in current
   evidence for the named revisions.
4. Confirm that `IMPL-PICKUP-SERVICE-LEGACY` keeps its own nonconforming result
   and gaps.
5. Trace the late controller result from implementation discovery through
   revised intent, named approval, implementation work, and evidence.
6. Check failure, permission, concurrency, time, recovery, secret, audit, and
   stale-evidence cases.
7. Route the Courier Console product from the repository index and follow its
   consumed pickup contract to the Parcel Pickup Coordinator's owning IDs.
8. Follow `PROF-PEAK-SITE` from the audit rule into evidence and confirm that
   the profile defines conditions rather than a threshold or passing result.
9. Follow `REF-CONTROLLER-OPEN-V7` from its governing pickup requirement to its
   checked-in fixture and evidence scope.
10. Follow the draft `REF-COURIER-STOP-CARD` from its governing requirements to
    the SVG and confirm that text keeps semantic and accessibility duties while
    the visual carries only its declared relationships.
11. Confirm that the pickup-site composition remains `Unknown` and cannot
    borrow the pickup-service component's `Conformant` result.

## 6. Links and IDs

1. Open every changed relative Markdown link and heading anchor.
2. Confirm that every referenced repository path exists.
3. List every semantic ID definition and check that no other rule defines the
   same ID.
4. Confirm that retired IDs remain findable and no writer reused one for another
   duty.
5. Confirm that each normative scenario extends an existing parent ID and uses
   the most specific ID in its evidence tag.
6. Check every Markdown table for the same number of cells in its header,
   separator, and data rows.

## 7. Vendor and tool independence

1. Search normative text for product, model, agent, language, framework,
   storage, and hosted-service names.
2. Replace any requirement that binds adopters to one vendor or tool unless the
   rule describes a vendor-neutral file or Git behavior that OpenIntent itself
   requires.
3. Read the complete method using rendered Markdown only. Confirm that no
   parser, schema, hidden prompt, or hosted service supplies required meaning.
4. Keep possible automation in [evolution.md](evolution.md) until project use
   proves that the method needs it.

## First public release gate

OpenIntent remains version 0.1 while maintainers revise it before publication.
The first public release also uses version 0.1. Before that release, a
maintainer records `PASS` for all seven audits, confirms that the status says
`Pre-publication draft`, and changes it to `Public draft` as part of the
publication change without increasing the version.
