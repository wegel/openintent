# CHG-<YYYYMMDD>-<NAME>: <Change title>

| Field | Value |
| --- | --- |
| ID | `CHG-<YYYYMMDD>-<NAME>` |
| Change state | Active |
| Intent checkpoint | Draft |
| Author | `<person or agent>` |
| Affected products | `<PROD IDs>` |
| Cross-product coordinator | `<person or not applicable>` |
| Product authority scopes | `<registry scopes>` |
| Created | `<YYYY-MM-DD>` |
| Target release | `<release, date, or none>` |
| Proposed intent revision | `<working-branch commit or pending>` |
| Accepted intent revision | `<accepted-branch commit or pending>` |
| Overlapping changes | `<IDs and acceptance order, or none>` |

## Why now

<!-- Name a user, operator, policy, incident, or opportunity. Do not start with a
component to build. -->

<Concrete need and evidence>

## Intended outcome

`<Actor>` can `<new or changed outcome>` while `<important preserved outcome or
invariant>` remains true.

## Non-goals

- **NON-GOAL:** `<nearby behavior this change will not add or alter>`

## Context packet

An implementer or reviewer should read:

- `intent/index.md`
- `<repository index and each affected product index>`
- `<affected capability>`
- `<linked glossary, quality, profile, reference, decision, or adjacent capability>`
- `<overlapping active changes or none>`

## Intent edits

<!-- Keep this table current while intent and implementation evolve. Edit the
canonical files on the same working branch when practical. Summarize; do not
copy full normative text. List a scenario when its conditions or results change
independently of its parent. -->

| Kind | Intent, profile, or reference IDs | Canonical file or artifact record | Summary |
| --- | --- | --- | --- |
| Add | `<new IDs>` | `<path>` | `<new product duty>` |
| Change | `<existing IDs>` | `<path>` | `<same continuing duty with changed wording, conditions, or bound>` |
| Retire | `<old IDs>` | `<path>` | `<removed duty and replacement, if any>` |
| Preserve | `<risk-adjacent IDs that evidence will check>` | `<path>` | `<behavior that must not regress>` |

## Implementation targets

<!-- Keep one row per target. Use Not applicable for an intent-only change that
will not implement behavior. Never combine targets with different revisions or
results. A checkpoint here covers the affected and preserved IDs in this
change; it does not by itself claim that the target meets every accepted rule in
the intent index. -->

| Target ID | Kind | Owner | Checkpoint | Implementation revision | Components or participants | Current deployed behavior | Latest evidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `IMPL-<NAME>` | `<component or composition>` | `<person or team>` | Not started | `<revision or not started>` | `<target and external-system revisions, or none>` | `<same as intent, concrete difference, or not deployed>` | `<path, link, or none yet>` |

## Compatibility and migration

- Existing users or clients: `<effect or none>`
- Existing data or in-flight work: `<effect or none>`
- External interfaces: `<effect or none>`
- Rollout order: `<constraint or none>`
- Recovery or rollback: `<actor, trigger, and result>`

## Risks

| Risk | Affected actor | Prevention or detection | Recovery owner |
| --- | --- | --- | --- |
| `<concrete failure>` | `<actor>` | `<rule, check, or monitor>` | `<owner>` |

## Assumptions

- **ASSUMPTION:** `<fact outside product control>`

## Open questions

<!-- A question that changes conformance blocks full intent acceptance. Use
Partially accepted when product authority accepted only the recorded subset. -->

| Question | Owner | Needed by | Blocks |
| --- | --- | --- | --- |
| `<concrete alternatives and consequence>` | `<person>` | `<date or gate>` | `<intent IDs or checkpoint>` |

## Approval record

| Review | Proposed revision or target | Intent IDs | Named approver or reviewer | Date | Result and notes |
| --- | --- | --- | --- | --- | --- |
| Intent review | `<commit>` | `<IDs>` | `<named person>` | `<YYYY-MM-DD>` | `<accepted, rejected, or changes requested>` |
| Evidence review | `IMPL-<NAME>` at `<revision>` | `<IDs>` | `<named reviewer>` | `<YYYY-MM-DD>` | `<Conforms, Does not conform, or Not determined>` |

For a cross-product change, keep a separate intent-review row for each product
authority scope. One product's approval does not accept another product's IDs.

## Completion rule

<!-- Keep the change Active while it owns pending implementation work. Complete
an intent-only change only when every target row is Not applicable or later work
moved to a linked change. -->

`<What must be true before this record has no required work left>`

## Next action

`<Actor or owner>` will `<bounded action>` by `<date or gate>`.
