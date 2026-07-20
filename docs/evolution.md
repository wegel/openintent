# Evolving OpenIntent

OpenIntent 0.1 deliberately starts as a Markdown and Git method. Tools should
follow demonstrated needs instead of deciding the method in advance.

OpenIntent remains version 0.1 through its first public release. Pre-publication
edits update the draft without inventing unpublished version numbers.

## Version path

OpenIntent uses major and minor versions:

- `0.x` versions are public drafts. They may change required artifacts or
  meanings after field use exposes a flaw.
- `1.0` will mark a stable core that maintainers expect adopters to carry
  forward.
- Later minor versions may add compatible guidance or optional artifacts.
- Later major versions may change conformance rules.

A project names the version it follows in `intent/index.md`. It may adopt newer
rules gradually and should record deliberate mixed-version use.

## Evidence needed before 1.0

Maintainers should seek reports from:

- new and existing products;
- small repositories and monorepos;
- at least several unrelated coding agents;
- teams with different Git review practices;
- stateful and concurrent systems;
- products with permission, privacy, accessibility, and reliability duties; and
- at least one implementation replacement or substantial rewrite.

Reports should name where an agent guessed, loaded too much context, confused
history with intent, or could not map evidence back to a requirement.
Reports should also show when implementation changed proposed intent, which work
paused, who accepted the new product choice, and whether the checkpoints helped
another participant continue.

## How a normative change should enter

A contributor describes a concrete failure, proposes exact rule text, updates
affected templates, and exercises the parcel locker example. Public review asks:

- Does the rule solve a demonstrated problem?
- Can a person follow it with Markdown and Git alone?
- Does it preserve vendor neutrality?
- Does it reduce or justify added context and artifact cost?
- Can current adopters migrate without losing intent history?
- Could an optional tool help without becoming the authority?

Maintainers record accepted normative changes in Git. Before the first public
release, they keep version 0.1. After that release, they update the version when
a normative change alters conformance. Editorial clarifications may keep the
current version when they do not change a conformance result.

## Likely optional tools

Field use may justify tools that:

- find duplicate IDs and broken links;
- check product ownership and cross-product contract routes;
- find permission or transition summaries without governing IDs;
- find overlapping active changes without an acceptance order;
- build a context packet from the intent index;
- show which requirements a change affects;
- check that evidence covers affected rules;
- compare an accepted requirement with recent test results;
- render state transitions and trace maps;
- help reviewers find stale conformance evidence;
- keep component and composition targets and their evidence scopes distinct;
- compare governed properties in normative supporting artifacts; or
- compare evidence conditions with named operating profiles.

Such a tool should read the same Markdown that people review. It should report
findings, not silently repair or reinterpret product intent.

## Extension rules

A future extension should:

1. declare the OpenIntent version it targets;
2. keep its data human-readable or provide a checked-in human-readable view;
3. avoid changing BCP 14 meanings;
4. avoid copying accepted intent into a vendor-owned store as the only source;
5. leave the repository usable when the extension is absent; and
6. identify generated files so reviewers know which source controls them.

## Why 0.1 has no schema

A schema would make required fields look precise before project use proves that
they carry stable meaning. It would also encourage early tools to reject useful
domain-specific forms.

OpenIntent 0.1 uses predictable metadata tables, headings, IDs, and links. A
future version can standardize a machine-readable view after several independent
tools and projects converge on the same semantics.

## Future formal methods

Projects may translate high-risk state and invariant rules into executable
models, temporal logic, property tests, or proof systems. OpenIntent only asks
that each formal statement link to a human-readable requirement and disclose its
assumptions.

If common mappings emerge, a later version may describe them. The Markdown
contract should remain readable to product owners and reviewers who do not use
the formal tool.

## Governance still to prove

Before publication, this draft uses repository reviews, maintainer review, and
Git history. After publication, the project also uses public issues and pull
requests. The project should not imitate a large standards body before it has a
community that needs one.

Before 1.0, contributors should propose clear rules for maintainership, conflict
resolution, security reports, appeals, and standard maturity. Those rules should
come from actual contribution patterns and should protect open participation.
